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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 5269ec74388fa9b09a4cceabad364d19409470df
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65699748"
---
# <a name="handle-a-concurrency-exception"></a>处理并发异常
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

并发异常 (<xref:System.Data.DBConcurrencyException>) 两个用户尝试同时更改相同的数据在数据库中时引发。 在本演练中，创建一个 Windows 应用程序，演示如何捕获<xref:System.Data.DBConcurrencyException>，找到导致此错误的行，并了解如何对其进行处理的策略。  
  
 本演练将指导你完成以下过程：  
  
1. 创建一个新**Windows 应用程序**项目。  
  
2. 创建新的数据集基于 Northwind`Customers`表。  
  
3. 创建一个具有窗体<xref:System.Windows.Forms.DataGridView>以显示数据。  
  
4. 使用中的数据填充数据集`Customers`Northwind 数据库中的表。  
  
5. 使用[Visual Database Tools](https://msdn.microsoft.com/6b145922-2f00-47db-befc-bf351b4809a1)在 Visual Studio 中直接访问`Customers`数据表和更改的记录。  
  
6. 为不同的值更改同一记录、 更新数据集，并尝试将所做的更改写入到数据库，这会导致引发并发错误。  
  
7. 捕获到的错误，则显示不同版本的记录，这样就允许用户确定要继续，并更新数据库，还是要取消更新。  
  
## <a name="prerequisites"></a>系统必备  
 若要完成本演练，你需要：  
  
- 访问 Northwind 示例数据库有权执行更新。
  
> [!NOTE]
> 对话框和菜单命令可能不同于所述的帮助，具体取决于您现用的设置或正在使用的版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## <a name="create-a-new-project"></a>创建新项目  
 通过创建新的 Windows 应用程序开始在演练。  
  
#### <a name="to-create-a-new-windows-application-project"></a>若要创建新的 Windows 应用程序项目  
  
1. 上**文件**菜单中，创建一个新项目。  
  
2. 在中**项目类型**窗格中，选择一种编程语言。  
  
3. 在中**模板**窗格中，选择**Windows 应用程序**。  
  
4. 将项目命名`ConcurrencyWalkthrough`，然后选择**确定**。  
  
     Visual Studio 将添加到项目**解决方案资源管理器**，并在设计器中显示新窗体。  
  
## <a name="create-the-northwind-dataset"></a>创建 Northwind 数据集  
 在本部分中，您将创建名为的数据集`NorthwindDataSet`。  
  
#### <a name="to-create-the-northwinddataset"></a>若要创建 NorthwindDataSet  
  
1. 上**数据**菜单中，选择**添加新数据源**。  
  
     “数据源配置”向导随即打开[](https://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f)。  
  
2. 上**选择数据源类型**屏幕上，选择**数据库**。  
  
3. 从可用连接列表中选择与 Northwind 示例数据库的连接。如果连接不可用的连接列表中，选择**新的连接**  
  
    > [!NOTE]
    > 如果您要连接到本地数据库文件，选择**否**当系统询问是否要将文件添加到你的项目。  
  
4. 上**将连接字符串保存到应用程序配置文件**屏幕上，选择**下一步**。  
  
5. 展开**表**节点，然后选择`Customers`表。 数据集的默认名称应为`NorthwindDataSet`。  
  
6. 选择**完成**将数据集添加到项目。  
  
## <a name="create-a-data-bound-datagridview-control"></a>创建数据绑定 DataGridView 控件  
 在本部分中，您将创建<xref:System.Windows.Forms.DataGridView>拖拽**客户**项从**数据源**拖到 Windows 窗体的窗口。  
  
#### <a name="to-create-a-datagridview-control-that-is-bound-to-the-customers-table"></a>若要创建绑定到客户表的 DataGridView 控件  
  
1. 上**数据**菜单中，选择**显示数据源**以打开**数据源窗口**。  
  
2. 在中**数据源**窗口中，展开**NorthwindDataSet**节点，并选择**客户**表。  
  
3. 选择表节点上的向下箭头，然后选择**DataGridView**下拉列表中。  
  
4. 将该表拖到窗体的空白区域。  
  
     一个<xref:System.Windows.Forms.DataGridView>名为控件`CustomersDataGridView`和一个<xref:System.Windows.Forms.BindingNavigator>名为`CustomersBindingNavigator`添加到窗体绑定到<xref:System.Windows.Forms.BindingSource>。这是在中，打开绑定到`Customers`表中`NorthwindDataSet`。  
  
## <a name="test-the-form"></a>测试窗体  
 现在可以测试窗体，以确保其行为符合预期到目前为止。  
  
#### <a name="to-test-the-form"></a>若要测试窗体  
  
1. 选择**F5**运行该应用程序  
  
     窗体将显示<xref:System.Windows.Forms.DataGridView>上的控件中的数据填充的`Customers`表。  
  
2. 上**调试**菜单中，选择**停止调试**。  
  
## <a name="handleconcurrency-errors"></a>Handleconcurrency 错误  
 如何处理错误的方式取决于用于管理你的应用程序的特定业务规则。 对于本演练中，我们使用以下策略作为示例了解如何处理并发错误等量。  
  
 Applicationpresents 具有三个版本记录的用户：  
  
- 数据库中的当前记录  
  
- 最早的记录加载到数据集  
  
- 中的数据集的建议的更改  
  
  然后，用户就能够使用建议的版本中，覆盖数据库，或取消更新刷新来自数据库的新值的数据集。  
  
#### <a name="to-enable-the-handling-of-concurrency-errors"></a>若要启用并发错误的处理  
  
1. 创建自定义错误处理程序。  
  
2. 向用户显示的选择。  
  
3. 处理用户的响应。  
  
4. 重新发送更新，或重置在数据集中的数据。  
  
### <a name="addcode-to-handle-the-concurrency-exception"></a>Addcode 来处理并发异常  
 如果你尝试要执行更新，并且引发了异常时，通常想要使用提供的引发的异常的信息执行某些操作。  
  
 在本部分中，您将添加代码，尝试更新数据库。你还处理任何<xref:System.Data.DBConcurrencyException>可能引发的以及任何其他异常。  
  
> [!NOTE]
> `CreateMessage`和`ProcessDialogResults`方法将添加在本演练后面。  
  
##### <a name="to-add-error-handling-for-the-concurrency-error"></a>若要添加的错误处理并发错误  
  
1. 添加以下代码`Form1_Load`方法：  
  
     [!code-csharp[VbRaddataConcurrency#1](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs#1)]
     [!code-vb[VbRaddataConcurrency#1](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb#1)]  
  
2. 替换`CustomersBindingNavigatorSaveItem_Click`方法来调用`UpdateDatabase`方法，使它看起来如下所示：  
  
     [!code-csharp[VbRaddataConcurrency#2](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs#2)]
     [!code-vb[VbRaddataConcurrency#2](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb#2)]  
  
### <a name="displaychoices-to-the-user"></a>向用户 Displaychoices  
 您刚的代码编写调用`CreateMessage`过程来向用户显示错误信息。 对于本演练中，使用一个消息框，以向用户显示该记录的不同版本。这使用户能够选择是否要覆盖记录的更改或取消编辑。 一旦用户选择消息框上的选项 （单击一个按钮），响应传递给`ProcessDialogResult`方法。  
  
##### <a name="to-create-the-message-to-display-to-the-user"></a>若要创建要向用户显示的消息  
  
- 通过添加以下代码创建的消息**代码编辑器**。 输入此代码下面`UpdateDatabase`方法。  
  
     [!code-csharp[VbRaddataConcurrency#4](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs#4)]
     [!code-vb[VbRaddataConcurrency#4](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb#4)]  
  
### <a name="process-the-users-response"></a>处理用户的响应  
 您还需要代码来处理用户的响应消息框。 选项，可使用建议的更改，覆盖当前数据库中的记录或放弃本地更改和刷新数据表与目前在数据库中的记录。 如果用户选择是，<xref:System.Data.DataTable.Merge%2A>与调用方法*preserveChanges*参数设置为`true`。 这将导致更新尝试将会成功，因为该记录的原始版本现在与数据库中的记录相匹配。  
  
##### <a name="to-process-the-user-input-from-the-message-box"></a>从 messagebox 中处理用户输入  
  
- 添加下面的代码已在上一节中添加的代码。  
  
     [!code-csharp[VbRaddataConcurrency#3](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs#3)]
     [!code-vb[VbRaddataConcurrency#3](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb#3)]  
  
## <a name="test-the-form"></a>测试窗体  
 现在可以测试窗体，以确保其行为符合预期。 若要模拟并发冲突需要填充 NorthwindDataSet 后更改数据库中的数据。  
  
#### <a name="to-test-the-form"></a>若要测试窗体  
  
1. 选择**F5**运行该应用程序。  
  
2. 在窗体显示后，使其继续运行，并切换到 Visual Studio IDE。  
  
3. 上**视图**菜单中，选择**服务器资源管理器**。  
  
4. 在中**服务器资源管理器**，展开连接应用程序使用，然后展开**表**节点。  
  
5. 右键单击**客户**表，，然后选择**显示表数据**。  
  
6. 在第一条记录 (`ALFKI`) 更改`ContactName`到`Maria Anders2`。  
  
    > [!NOTE]
    > 导航到不同的行以提交更改。  
  
7. 切换到`ConcurrencyWalkthrough`的运行窗体。  
  
8. 在窗体上的第一个记录中 (`ALFKI`)，更改`ContactName`到`Maria Anders1`。  
  
9. 选择“保存”按钮。  
  
     会引发并发错误，并显示消息框。  
  
10. 选择**否**取消更新并使用当前数据库中的值更新数据集。 选择**是**建议的值写入数据库。
  
## <a name="see-also"></a>请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)