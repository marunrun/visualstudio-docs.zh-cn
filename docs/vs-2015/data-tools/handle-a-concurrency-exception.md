---
title: 处理并发异常 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- concurrency control, exceptions
- datasets [Visual Basic], errors
- exception handling, concurrency issues
- data concurrency, walkthroughs
- updating datasets, errors
- concurrency control, walkthroughs
ms.assetid: 73ee9759-0a90-48a9-bf7b-9d6fc17bff93
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1b3f9bdaf5107f805100b938212128d42c0263dd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670035"
---
# <a name="handle-a-concurrency-exception"></a>处理并发异常
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

<xref:System.Data.DBConcurrencyException>当两个用户尝试同时更改数据库中的相同数据时，将引发并发异常 () 。 在本演练中，您将创建一个 Windows 应用程序，该应用程序演示如何捕获 <xref:System.Data.DBConcurrencyException> ，找到导致错误的行，并学习如何处理它的策略。

 本演练将引导你完成以下过程：

1. 创建新的 **Windows 应用程序** 项目。

2. 基于 Northwind 表创建新的数据集 `Customers` 。

3. 使用创建窗体 <xref:System.Windows.Forms.DataGridView> 以显示数据。

4. 使用 Northwind 数据库的表中的数据填充数据集 `Customers` 。

5. 使用 Visual Studio 中的 [Visual Database Tools](https://msdn.microsoft.com/6b145922-2f00-47db-befc-bf351b4809a1) 直接访问数据表 `Customers` 和更改记录。

6. 将相同的记录更改为其他值，更新数据集，并尝试将更改写入数据库，这将导致引发并发错误。

7. 捕获错误，然后显示记录的不同版本，使用户能够确定是继续还是更新数据库，或取消更新。

## <a name="prerequisites"></a>先决条件
 若要完成本演练，你需要：

- 访问 Northwind 示例数据库，具有执行更新的权限。

> [!NOTE]
> 你看到的对话框和菜单命令可能与 "帮助" 中描述的不同，具体取决于你当前使用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。

## <a name="create-a-new-project"></a>创建新项目
 首先，创建一个新的 Windows 应用程序。

#### <a name="to-create-a-new-windows-application-project"></a>创建新的 Windows 应用程序项目

1. 在 " **文件** " 菜单上，创建一个新项目。

2. 在 " **项目类型** " 窗格中，选择一种编程语言。

3. 在“模板”窗格中，选择“Windows 应用程序”。 

4. 为该项目命名 `ConcurrencyWalkthrough` ，然后选择 **"确定"**。

     Visual Studio 会将项目添加到 **解决方案资源管理器** ，并在设计器中显示一个新窗体。

## <a name="create-the-northwind-dataset"></a>创建 Northwind 数据集
 在本部分中，将创建一个名为的数据集 `NorthwindDataSet` 。

#### <a name="to-create-the-northwinddataset"></a>创建 NorthwindDataSet

1. 在 " **数据** " 菜单上，选择 " **添加新数据源**"。

     " [数据源配置向导](https://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f) " 将打开。

2. 在 " **选择数据源类型**" 屏幕上，选择 " **数据库**"。

3. 从可用连接的列表中选择与 Northwind 示例数据库的连接。如果连接列表中的连接不可用，请选择 "**新建连接**"

    > [!NOTE]
    > 如果要连接到本地数据库文件，请在询问是否要将文件添加到项目时，选择 " **否** "。

4. 在 "将 **连接字符串保存到应用程序配置文件**" 屏幕上，选择 " **下一步**"。

5. 展开 " **表** " 节点并选择 `Customers` 表。 数据集的默认名称应为 `NorthwindDataSet` 。

6. 选择 " **完成** " 将数据集添加到项目。

## <a name="create-a-data-bound-datagridview-control"></a>创建数据绑定 DataGridView 控件
 在本部分中，将 <xref:System.Windows.Forms.DataGridView> 通过将 " **客户** " 项从 " **数据源** " 窗口拖到 Windows 窗体来创建。

#### <a name="to-create-a-datagridview-control-that-is-bound-to-the-customers-table"></a>创建绑定到 Customers 表的 DataGridView 控件

1. 在 " **数据** " 菜单上，选择 " **显示数据源** " 以打开 " **数据源" 窗口**。

2. 在 " **数据源** " 窗口中，展开 " **NorthwindDataSet** " 节点，然后选择 " **Customers** " 表。

3. 选择 "表" 节点上的向下箭头，然后在下拉列表中选择 " **DataGridView** "。

4. 将该表拖到窗体的空白区域。

     名为的 <xref:System.Windows.Forms.DataGridView> 控件和名为的控件 `CustomersDataGridView` <xref:System.Windows.Forms.BindingNavigator> `CustomersBindingNavigator` 添加到绑定到的窗体中 <xref:System.Windows.Forms.BindingSource> 。这是在中，它将绑定到 `Customers` 中的表 `NorthwindDataSet` 。

## <a name="test-the-form"></a>测试窗体
 你现在可以测试窗体，确保它在此点之前的行为与预期相同。

#### <a name="to-test-the-form"></a>测试窗体

1. 选择 **F5** 以运行应用程序

     窗体上将显示一个 <xref:System.Windows.Forms.DataGridView> 控件，其中填充了表中的数据 `Customers` 。

2. 在 " **调试** " 菜单上，选择 "**停止调试**"。

## <a name="handleconcurrency-errors"></a>Handleconcurrency 错误
 处理错误的方式取决于控制应用程序的特定业务规则。 对于本演练，我们将使用以下策略作为 tohandle 并发错误的示例。

 将用户 applicationpresents 记录的三个版本：

- 数据库中的当前记录

- 加载到数据集中的原始记录

- 数据集中的建议更改

  然后，用户可以用建议的版本覆盖数据库，或取消更新，并通过数据库中的新值刷新数据集。

#### <a name="to-enable-the-handling-of-concurrency-errors"></a>启用并发错误处理

1. 创建自定义错误处理程序。

2. 向用户显示选择。

3. 处理用户的响应。

4. 重新发送更新，或重置数据集中的数据。

### <a name="addcode-to-handle-the-concurrency-exception"></a>Addcode 处理并发异常
 当你尝试执行更新并引发异常时，通常需要使用引发的异常提供的信息来执行某些操作。

 在本部分中，将添加尝试更新数据库的代码。还处理 <xref:System.Data.DBConcurrencyException> 可能引发的任何，以及任何其他异常。

> [!NOTE]
> `CreateMessage` `ProcessDialogResults` 稍后将在本演练中添加和方法。

##### <a name="to-add-error-handling-for-the-concurrency-error"></a>为并发错误添加错误处理

1. 在方法下面添加以下代码 `Form1_Load` ：

     [!code-csharp[VbRaddataConcurrency#1](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs#1)]
     [!code-vb[VbRaddataConcurrency#1](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb#1)]

2. 替换 `CustomersBindingNavigatorSaveItem_Click` 方法以调用方法，如下所示 `UpdateDatabase` ：

     [!code-csharp[VbRaddataConcurrency#2](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs#2)]
     [!code-vb[VbRaddataConcurrency#2](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb#2)]

### <a name="displaychoices-to-the-user"></a>Displaychoices 用户
 刚编写的代码调用 `CreateMessage` 过程向用户显示错误信息。 对于本演练，您将使用消息框向用户显示该记录的不同版本。这样，用户就可以选择是用更改覆盖记录还是取消编辑。 一旦用户选择某个选项 (单击消息框上的按钮) ，就会将响应传递到该 `ProcessDialogResult` 方法。

##### <a name="to-create-the-message-to-display-to-the-user"></a>创建向用户显示的消息

- 通过将以下代码添加到 **代码编辑器**来创建消息。 在方法下面输入此代码 `UpdateDatabase` 。

     [!code-csharp[VbRaddataConcurrency#4](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs#4)]
     [!code-vb[VbRaddataConcurrency#4](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb#4)]

### <a name="process-the-users-response"></a>处理用户的响应
 还需要代码来处理用户对消息框的响应。 这些选项可以用建议的更改覆盖数据库中的当前记录，也可以放弃本地更改并刷新包含数据库中当前记录的数据表。 如果用户选择 "是"，则 <xref:System.Data.DataTable.Merge%2A> 会调用方法，并将 *preserveChanges* 参数设置为 `true` 。 这会导致更新尝试成功，因为原始版本的记录现在与数据库中的记录匹配。

##### <a name="to-process-the-user-input-from-the-message-box"></a>处理消息框中的用户输入

- 在上一部分中添加的代码下面添加以下代码。

     [!code-csharp[VbRaddataConcurrency#3](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs#3)]
     [!code-vb[VbRaddataConcurrency#3](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb#3)]

## <a name="test-the-form"></a>测试窗体
 你现在可以对窗体进行测试，以确保它按预期方式运行。 若要模拟并发冲突，需要在填写 NorthwindDataSet 后更改数据库中的数据。

#### <a name="to-test-the-form"></a>测试窗体

1. 选择 **F5** 以运行应用程序。

2. 窗体显示后，使其保持运行状态，并切换到 Visual Studio IDE。

3. 在“视图”菜单中，选择“服务器资源管理器”。********

4. 在 **服务器资源管理器**中，展开应用程序正在使用的连接，然后展开 " **表** " 节点。

5. 右键单击 **Customers** 表，然后选择 " **显示表数据**"。

6. 在第一条记录中 (`ALFKI`) "更改 `ContactName` 为" `Maria Anders2` 。

    > [!NOTE]
    > 导航到不同的行以提交更改。

7. 切换到 `ConcurrencyWalkthrough` 正在运行的窗体。

8. 在 () 窗体上的第一条记录中 `ALFKI` ，将更改 `ContactName` 为 `Maria Anders1` 。

9. 选择“保存”按钮。

     引发并发错误，并显示消息框。

10. 选择 " **否** " 将取消更新并用数据库中当前的值更新数据集。 选择 **"是"** 将建议的值写入数据库。

## <a name="see-also"></a>另请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)