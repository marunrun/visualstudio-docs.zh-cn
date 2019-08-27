---
title: 处理并发异常
ms.date: 09/11/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- concurrency control, exceptions
- datasets [Visual Basic], errors
- exception handling, concurrency issues
- data concurrency, walkthroughs
- updating datasets, errors
- concurrency control, walkthroughs
ms.assetid: 73ee9759-0a90-48a9-bf7b-9d6fc17bff93
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: a8e14a53719d4913bcc04bcb2b702ca4ec4a8c55
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62566737"
---
# <a name="handle-a-concurrency-exception"></a>处理并发异常

并发异常 (<xref:System.Data.DBConcurrencyException?displayProperty=fullName>) 两个用户尝试同时更改相同的数据在数据库中时引发。 在本演练中，创建一个 Windows 应用程序，演示如何捕获<xref:System.Data.DBConcurrencyException>，找到导致此错误的行，并了解如何对其进行处理的策略。

本演练将指导你完成以下过程：

1. 创建新的 **Windows 窗体应用程序**项目。

2. 创建基于 Northwind Customers 表的新数据集。

3. 创建一个具有窗体<xref:System.Windows.Forms.DataGridView>以显示数据。

4. 使用 Northwind 数据库中的 Customers 表中的数据填充数据集。

5. 使用**显示表数据**中的功能**服务器资源管理器**能够访问客户表的数据和更改记录。

6. 为不同的值更改同一记录、 更新数据集，并尝试将所做的更改写入到数据库，这会导致引发并发错误。

7. 捕获到的错误，然后显示不同版本的记录，这样就允许用户确定是否要继续，并更新数据库，或取消更新。

## <a name="prerequisites"></a>系统必备

本演练使用 SQL Server Express LocalDB 和 Northwind 示例数据库。

1. 如果您没有 SQL Server Express LocalDB，安装它从[SQL Server Express 下载页](https://www.microsoft.com/sql-server/sql-server-editions-express)，或通过**Visual Studio 安装程序**。 在中**Visual Studio 安装程序**，可以作为的一部分安装 SQL Server Express LocalDB**数据存储和处理**工作负荷，或作为单个组件。

2. 通过执行以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中打开**SQL Server 对象资源管理器**窗口。 (SQL Server 对象资源管理器安装的一部分**数据存储和处理**Visual Studio 安装程序中的工作负载。)展开**SQL Server**节点。 LocalDB 实例上右键单击并选择**新查询**。

       查询编辑器窗口随即打开。

    2. 复制[Northwind Transact SQL 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)到剪贴板。 此 T-SQL 脚本从零开始创建 Northwind 数据库，并使用数据填充它。

    3. 将 T-SQL 脚本粘贴到查询编辑器，然后选择**Execute**按钮。

       后不久，查询完成运行并创建 Northwind 数据库。

## <a name="create-a-new-project"></a>创建新项目

首先，创建新的 Windows 窗体应用程序：

1. 在 Visual Studio 中，在**文件**菜单中，选择**新建** > **项目**。

2. 展开**Visual C#** 或**Visual Basic**在左侧窗格中，然后选择**Windows 桌面**。

3. 在中间窗格中，选择**Windows 窗体应用**项目类型。

4. 将项目命名**ConcurrencyWalkthrough**，然后选择**确定**。

     **ConcurrencyWalkthrough**创建项目并将其添加到**解决方案资源管理器**，并在设计器中打开一个新窗体。

## <a name="create-the-northwind-dataset"></a>创建 Northwind 数据集

接下来，创建名为的数据集**NorthwindDataSet**:

1. 上**数据**菜单中，选择**添加新数据源**。

   “数据源配置”向导随即打开。

2. 上**选择数据源类型**屏幕上，选择**数据库**。

   ![在 Visual Studio 中的数据源配置向导](media/data-source-configuration-wizard.png)

3. 从可用连接列表中选择与 Northwind 示例数据库的连接。 如果连接不可用的连接列表中，选择**新的连接**。

    > [!NOTE]
    > 如果要连接到本地数据库文件，选择**否**当系统询问是否要将文件添加到你的项目。

4. 上**将连接字符串保存到应用程序配置文件**屏幕上，选择**下一步**。

5. 展开**表**节点，然后选择**客户**表。 数据集的默认名称应**NorthwindDataSet**。

6. 选择**完成**将数据集添加到项目。

## <a name="create-a-data-bound-datagridview-control"></a>创建数据绑定 DataGridView 控件

在本部分中，您将创建<xref:System.Windows.Forms.DataGridView?displayProperty=nameWithType>拖拽**客户**项从**数据源**拖到 Windows 窗体的窗口。

1. 若要打开**数据源**窗口，然后在**数据**菜单中，选择**显示数据源**。

2. 在中**数据源**窗口中，展开**NorthwindDataSet**节点，并选择**客户**表。

3. 选择表节点上的向下箭头，然后选择**DataGridView**下拉列表中。

4. 将该表拖到窗体的空白区域。

     一个<xref:System.Windows.Forms.DataGridView>名为控件**CustomersDataGridView**，和一个<xref:System.Windows.Forms.BindingNavigator>名为**CustomersBindingNavigator**，将添加到窗体绑定到<xref:System.Windows.Forms.BindingSource>。 这反过来，绑定到 NorthwindDataSet 中的 Customers 表。

## <a name="test-the-form"></a>测试窗体

现在可以测试窗体，以确保其行为符合预期到目前为止：

1. 选择**F5**运行该应用程序。

     窗体将出现与<xref:System.Windows.Forms.DataGridView>上填充的客户表中的数据的控件。

2. 上**调试**菜单中，选择**停止调试**。

## <a name="handle-concurrency-errors"></a>处理并发错误

如何处理错误取决于用于管理你的应用程序的特定业务规则。 对于本演练中，我们使用以下策略作为一个示例，用于如何处理并发错误。

应用程序向用户提供的记录的三个版本：

- 数据库中的当前记录

- 最早的记录加载到数据集

- 中的数据集的建议的更改

然后，用户就能够使用建议的版本中，覆盖数据库，或取消更新刷新来自数据库的新值的数据集。

### <a name="to-enable-the-handling-of-concurrency-errors"></a>若要启用并发错误的处理

1. 创建自定义错误处理程序。

2. 向用户显示的选择。

3. 处理用户的响应。

4. 重新发送更新，或重置在数据集中的数据。

### <a name="add-code-to-handle-the-concurrency-exception"></a>添加代码以处理并发异常

如果你尝试要执行更新，并且会引发的异常，你通常想要使用提供的引发的异常的信息执行某些操作。 在本部分中，您将添加代码，尝试更新数据库。 你还处理任何<xref:System.Data.DBConcurrencyException>，可能会引发，以及任何其他异常。

> [!NOTE]
> `CreateMessage`和`ProcessDialogResults`稍后的演练中添加方法。

1. 添加以下代码`Form1_Load`方法：

   [!code-csharp[VbRaddataConcurrency#1](../data-tools/codesnippet/CSharp/handle-a-concurrency-exception_1.cs)]
   [!code-vb[VbRaddataConcurrency#1](../data-tools/codesnippet/VisualBasic/handle-a-concurrency-exception_1.vb)]

2. 替换`CustomersBindingNavigatorSaveItem_Click`方法来调用`UpdateDatabase`方法，使它看起来如下所示：

   [!code-csharp[VbRaddataConcurrency#2](../data-tools/codesnippet/CSharp/handle-a-concurrency-exception_2.cs)]
   [!code-vb[VbRaddataConcurrency#2](../data-tools/codesnippet/VisualBasic/handle-a-concurrency-exception_2.vb)]

### <a name="display-choices-to-the-user"></a>向用户显示的选项

您刚的代码编写调用`CreateMessage`过程来向用户显示错误信息。 对于本演练中，使用一个消息框，以向用户显示该记录的不同版本。 这使用户能够选择是否要覆盖记录的更改或取消编辑。 一旦用户选择消息框上的选项 （单击一个按钮），响应传递给`ProcessDialogResult`方法。

通过添加以下代码创建的消息**代码编辑器**。 输入此代码下面`UpdateDatabase`方法：

[!code-csharp[VbRaddataConcurrency#4](../data-tools/codesnippet/CSharp/handle-a-concurrency-exception_3.cs)]
[!code-vb[VbRaddataConcurrency#4](../data-tools/codesnippet/VisualBasic/handle-a-concurrency-exception_3.vb)]

### <a name="process-the-users-response"></a>处理用户的响应

您还需要代码来处理用户的响应消息框。 选项，可使用建议的更改，覆盖当前数据库中的记录或放弃本地更改和刷新数据表与目前在数据库中的记录。 如果用户选择**是**，则<xref:System.Data.DataTable.Merge%2A>方法调用与*preserveChanges*参数设置为**true**。 这将导致更新尝试将会成功，因为该记录的原始版本现在与数据库中的记录相匹配。

添加下面的代码已在上一节中添加以下代码：

[!code-csharp[VbRaddataConcurrency#3](../data-tools/codesnippet/CSharp/handle-a-concurrency-exception_4.cs)]
[!code-vb[VbRaddataConcurrency#3](../data-tools/codesnippet/VisualBasic/handle-a-concurrency-exception_4.vb)]

## <a name="test-the-form"></a>测试窗体

现在可以测试窗体，以确保其行为符合预期。 若要模拟并发冲突，请填充 NorthwindDataSet 后更改数据库中的数据。

1. 选择**F5**运行该应用程序。

2. 在窗体显示后，使其继续运行，并切换到 Visual Studio IDE。

3. 上**视图**菜单中，选择**服务器资源管理器**。

4. 在中**服务器资源管理器**，展开连接应用程序使用，然后展开**表**节点。

5. 右键单击**客户**表，，然后选择**显示表数据**。

6. 在第一条记录 (**ALFKI**)，更改**ContactName**到**Maria Anders2**。

    > [!NOTE]
    > 导航到不同的行以提交更改。

7. 切换到 ConcurrencyWalkthrough 的正在运行窗体。

8. 在窗体上的第一个记录中 (**ALFKI**)，更改**ContactName**到**Maria Anders1**。

9. 选择“保存”按钮。

     会引发并发错误，并显示消息框。

   选择**否**取消更新并使用当前数据库中的值更新数据集。 选择**是**建议的值写入数据库。

## <a name="see-also"></a>请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)