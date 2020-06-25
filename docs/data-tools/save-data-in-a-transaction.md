---
title: 演练：在事务中保存数据
ms.date: 09/08/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- System.Transactions namespace
- data [Visual Studio], saving in a transaction
- transactions, saving data
- Transactions namespace
- saving data
ms.assetid: 80260118-08bc-4b37-bfe5-9422ee7a1e4e
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: caeb06ac3f38293b493463ff456e222f148ef93a
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281625"
---
# <a name="walkthrough-save-data-in-a-transaction"></a>演练：在事务中保存数据

本演练演示如何使用命名空间在事务中保存数据 <xref:System.Transactions> 。 在本演练中，你将创建一个 Windows 窗体应用程序。 您将使用 "数据源配置向导" 创建 Northwind 示例数据库中两个表的数据集。 你将在 Windows 窗体中添加数据绑定控件，你将修改 BindingNavigator 的 "保存" 按钮的代码以更新 TransactionScope 内的数据库。

## <a name="prerequisites"></a>先决条件

本演练使用 SQL Server Express LocalDB 和 Northwind 示例数据库。

1. 如果没有 SQL Server Express 的 LocalDB，请从[SQL Server Express 下载 "页](https://www.microsoft.com/sql-server/sql-server-editions-express)或通过**Visual Studio 安装程序**安装它。 在 Visual Studio 安装程序中，SQL Server Express LocalDB 可以作为 **.net 桌面开发**工作负荷的一部分安装，也可以作为单个组件安装。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中，打开 " **SQL Server 对象资源管理器**" 窗口。 （SQL Server 对象资源管理器作为 Visual Studio 安装程序中的**数据存储和处理**工作负荷的一部分安装。）展开 " **SQL Server** " 节点。 右键单击 LocalDB 实例，然后选择 "**新建查询**"。

       此时将打开查询编辑器窗口。

    2. 将[Northwind transact-sql 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-sql 脚本从头开始创建 Northwind 数据库，并用数据填充它。

    3. 将 T-sql 脚本粘贴到查询编辑器中，然后选择 "**执行**" 按钮。

       一小段时间后，查询将完成运行，并创建 Northwind 数据库。

## <a name="create-a-windows-forms-application"></a>创建 Windows 窗体应用程序

第一步是创建**Windows 窗体应用程序**。

1. 在 Visual Studio 的“文件”菜单中，依次选择“新建” > “项目”    。

2. 在左侧窗格中展开 " **Visual c #** " 或 " **Visual Basic** "，然后选择 " **Windows 桌面**"。

3. 在中间窗格中，选择 " **Windows 窗体应用程序**" 项目类型。

4. 将项目命名为**SavingDataInATransactionWalkthrough**，然后选择 **"确定"**。

     创建“SavingDataInATransactionWalkthrough”项目并将其添加到“解决方案资源管理器”中********。

## <a name="create-a-database-data-source"></a>创建数据库数据源

此步骤使用 "**数据源配置向导**" 创建基于 `Customers` `Orders` Northwind 示例数据库中的和表的数据源。

1. 若要打开 "**数据源**" 窗口，请在 "**数据**" 菜单上选择 "**显示数据源**"。

2. 在“数据源”窗口，选择“添加新数据源”以启动“数据源配置”向导************。

3. 在 "**选择数据源类型**" 屏幕上，选择 "**数据库**"，然后选择 "**下一步**"。

4. 在 "**选择你的数据连接**" 屏幕上，执行以下操作之一：

    - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。

         \- 或 -

    - 选择“新建连接”以启动“添加/修改连接”对话框，并创建到 Northwind 数据库的连接********。

5. 如果数据库需要密码，请选择该选项以包括敏感数据，然后选择 "**下一步**"。

6. 在 "将**连接字符串保存到应用程序配置文件**" 屏幕上，选择 "**下一步**"。

7. 在 "**选择数据库对象**" 屏幕上，展开 "**表**" 节点。

8. 选择 `Customers` 和 `Orders` 表，然后选择 "**完成**"。

     将“NorthwindDataSet”添加到项目后，“数据源”窗口即会显示 `Customers` 和 `Orders` 表********。

## <a name="add-controls-to-the-form"></a>向窗体添加控件

可以通过将项从 "**数据源**" 窗口拖到窗体上来创建数据绑定控件。

1. 在 "**数据源**" 窗口中，展开 " **Customers** " 节点。

2. 将主“Customers”节点从“数据源”窗口拖到“Form1”上************。

   用于导航记录的 <xref:System.Windows.Forms.DataGridView> 控件和工具栏（<xref:System.Windows.Forms.BindingNavigator>）将显示在窗体上。 [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、、 `CustomersTableAdapter` <xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator> 显示在组件栏中。

3. 将相关的 " **orders** " 节点（而非 "主**订单**" 节点，但 " **Fax** " 列下的相关子表节点）拖到**CustomersDataGridView**下的窗体中。

   窗体上显示一个 <xref:System.Windows.Forms.DataGridView>。 `OrdersTableAdapter`并 <xref:System.Windows.Forms.BindingSource> 显示在组件栏中。

## <a name="add-a-reference-to-the-systemtransactions-assembly"></a>添加对 System.web 程序集的引用

事务使用 <xref:System.Transactions> 命名空间。 默认情况下，没有添加对 system.transactions 程序集的项目引用，因此你需要手动将其添加。

### <a name="to-add-a-reference-to-the-systemtransactions-dll-file"></a>添加对 System.Transactions DLL 文件的引用

1. 在“项目”菜单中，选择“添加引用”。********

2. 选择 "**系统事务**" （位于 " **.net** " 选项卡上），然后选择 **"确定"**。

     将“System.Transactions”的引用添加到项目****。

## <a name="modify-the-code-in-the-bindingnavigators-saveitem-button"></a>修改 BindingNavigator 的 "SaveItem" 按钮中的代码

对于拖放到窗体上的第一个表，默认情况下，会将代码添加到 `click` 上的 "保存" 按钮的事件中 <xref:System.Windows.Forms.BindingNavigator> 。 你需要手动添加代码以更新所有附加的表。 对于本演练，我们将重构保存按钮的单击事件处理程序中的现有保存代码。 另外，还创建了一些方法，以根据是否需要添加或删除行来提供特定的更新功能。

### <a name="to-modify-the-auto-generated-save-code"></a>修改自动生成的保存代码

1. 选择**CustomersBindingNavigator**上的 "**保存**" 按钮（带有软盘图标的按钮）。

2. 将 `CustomersBindingNavigatorSaveItem_Click` 方法替换为以下代码：

     [!code-vb[VbRaddataSaving#4](../data-tools/codesnippet/VisualBasic/save-data-in-a-transaction_1.vb)]
     [!code-csharp[VbRaddataSaving#4](../data-tools/codesnippet/CSharp/save-data-in-a-transaction_1.cs)]

对相关数据的协调更改的顺序如下：

- 删除子记录。 （在这种情况下，从表中删除记录 `Orders` 。）

- 删除父记录。 （在这种情况下，从表中删除记录 `Customers` 。）

- 插入父记录。 （在这种情况下，请在表中插入记录 `Customers` 。）

- 插入子记录。 （在这种情况下，请在表中插入记录 `Orders` 。）

### <a name="to-delete-existing-orders"></a>删除现有顺序

- 将以下 `DeleteOrders` 方法添加到“Form1”****：

     [!code-vb[VbRaddataSaving#5](../data-tools/codesnippet/VisualBasic/save-data-in-a-transaction_2.vb)]
     [!code-csharp[VbRaddataSaving#5](../data-tools/codesnippet/CSharp/save-data-in-a-transaction_2.cs)]

### <a name="to-delete-existing-customers"></a>删除现有客户

- 将以下 `DeleteCustomers` 方法添加到“Form1”****：

     [!code-vb[VbRaddataSaving#6](../data-tools/codesnippet/VisualBasic/save-data-in-a-transaction_3.vb)]
     [!code-csharp[VbRaddataSaving#6](../data-tools/codesnippet/CSharp/save-data-in-a-transaction_3.cs)]

### <a name="to-add-new-customers"></a>添加新客户

- 将以下 `AddNewCustomers` 方法添加到“Form1”****：

     [!code-vb[VbRaddataSaving#7](../data-tools/codesnippet/VisualBasic/save-data-in-a-transaction_4.vb)]
     [!code-csharp[VbRaddataSaving#7](../data-tools/codesnippet/CSharp/save-data-in-a-transaction_4.cs)]

### <a name="to-add-new-orders"></a>添加新顺序

- 将以下 `AddNewOrders` 方法添加到“Form1”****：

     [!code-vb[VbRaddataSaving#8](../data-tools/codesnippet/VisualBasic/save-data-in-a-transaction_5.vb)]
     [!code-csharp[VbRaddataSaving#8](../data-tools/codesnippet/CSharp/save-data-in-a-transaction_5.cs)]

## <a name="run-the-application"></a>运行应用程序

按 **F5** 运行该应用程序。

## <a name="see-also"></a>另请参阅

- [如何使用事务保存数据](../data-tools/save-data-by-using-a-transaction.md)
- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
