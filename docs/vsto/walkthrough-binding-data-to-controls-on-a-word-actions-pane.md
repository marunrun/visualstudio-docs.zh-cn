---
title: 演练：将数据绑定到 Word 操作窗格上的控件
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], data binding
- actions panes [Office development in Visual Studio], data binding
- data binding [Office development in Visual Studio], smart documents
- data binding [Office development in Visual Studio], actions panes
- actions panes [Office development in Visual Studio], binding controls
- smart documents [Office development in Visual Studio], data binding
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 05df38bf6056b392c0b991617316ba2c1c657306
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91585062"
---
# <a name="walkthrough-bind-data-to-controls-on-a-word-actions-pane"></a>演练：将数据绑定到 Word 操作窗格上的控件
  本演练演示如何将数据绑定到 Word 中操作窗格上的控件。 控件演示 SQL Server 数据库中表之间的主/从关系。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 本演练演示以下任务：

- 使用绑定到数据 Windows 窗体控件创建操作窗格。

- 使用主/从关系在控件中显示数据。

- 当应用程序打开时显示操作窗格。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 或 [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

- 使用 Northwind SQL Server 示例数据库访问服务器。

- 用于读取和写入 SQL Server 数据库的权限。

## <a name="create-the-project"></a>创建项目
 第一步是创建 Word 文档项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 使用 " **我的 Word 操作" 窗格**创建 word 文档项目。 在向导中，选择 " **创建新文档**"。

     有关详细信息，请参阅 [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 将在设计器中打开新的 Word 文档，并将 " **我的 Word 操作" 窗格** 项目添加到 **解决方案资源管理器**。

## <a name="add-controls-to-the-actions-pane"></a>向操作窗格添加控件
 对于本演练，需要一个包含数据绑定 Windows 窗体控件的操作窗格控件。 将数据源添加到项目，然后将控件从 " **数据源** " 窗口拖到 "操作" 窗格控件。

### <a name="to-add-an-actions-pane-control"></a>添加操作窗格控件

1. 在**解决方案资源管理器**中选择 "**我的 Word 操作" 窗格**项目。

2. 在 **“项目”** 菜单上，单击 **“添加新项”**。

3. 在 " **添加新项** " 对话框中，选择 " **操作窗格控件**"，将其命名为 **ActionsControl**，然后单击 " **添加**"。

### <a name="to-add-a-data-source-to-the-project"></a>向项目添加数据源

1. 如果 "**数据源**" 窗口不可见，请在菜单栏上选择 "**查看**  >  **其他 Windows**  >  **数据源**"，将其显示出来。

   > [!NOTE]
   > 如果 " **显示数据源** " 不可用，请单击 Word 文档，然后重新检查。

2. 单击 " **添加新数据源** " 以启动 " **数据源配置向导**"。

3. 选择 **数据库** ，然后单击 " **下一步**"。

4. 选择与 Northwind 示例 SQL Server 数据库的数据连接，或使用 " **新建连接** " 按钮添加新连接。

5. 单击“下一步”。

6. 清除 "保存连接" 选项，然后单击 " **下一步**"。

7. 展开 "**数据库对象**" 窗口中的 "**表**" 节点。

8. 选中 " **供应商** " 和 " **产品** " 表旁边的复选框。

9. 单击“完成”。

   向导将 " **供应商** 表和 **产品** " 表添加到 " **数据源** " 窗口。 它还将一个类型化数据集添加到你的项目中，该数据集在 **解决方案资源管理器**中可见。

### <a name="to-add-data-bound-windows-forms-controls-to-an-actions-pane-control"></a>向操作窗格控件添加数据绑定 Windows 窗体控件

1. 在 " **数据源** " 窗口中，展开 " **供应商** " 表。

2. 单击 " **公司名称** " 节点上的下拉箭头，然后选择 " **ComboBox**"。

3. 将 " **公司名称** " 从 " **数据源** " 窗口拖到 "操作" 窗格控件。

     在 <xref:System.Windows.Forms.ComboBox> 操作窗格控件上创建控件。 同时，已 <xref:System.Windows.Forms.BindingSource> 命名的 `SuppliersBindingSource` 、表适配器和将 <xref:System.Data.DataSet> 添加到组件栏中的项目。

4. 选择 `SuppliersBindingNavigator` **组件** 栏并按 **Delete**。 在本演练中，您将不会使用 `SuppliersBindingNavigator` 。

    > [!NOTE]
    > 删除 `SuppliersBindingNavigator` 不会删除为其生成的所有代码。 您可以删除此代码。

5. 移动组合框，使其位于标签下面，将 " **Size** " 属性更改为 **171，21**。

6. 在 "**数据源**" 窗口中，展开作为 "**供应商**" 表的子表的 "**产品**" 表。

7. 单击 " **ProductName** " 节点上的下拉箭头，然后选择 " **ListBox**"。

8. 将 " **ProductName** " 拖到 "操作" 窗格控件。

     在 <xref:System.Windows.Forms.ListBox> 操作窗格控件上创建控件。 同时，已 <xref:System.Windows.Forms.BindingSource> 命名的 `ProductBindingSource` 和表适配器将添加到组件栏中的项目。

9. 移动列表框，使其位于标签下，并将 " **Size** " 属性更改为 " **171，95**"。

10. 将 <xref:System.Windows.Forms.Button> 从 " **工具箱** " 拖动到 "操作" 窗格控件，并将其放置在列表框的下方。

11. 右键单击 <xref:System.Windows.Forms.Button> ，然后单击快捷菜单上的 " **属性** "，并更改以下属性。

    |properties|值|
    |--------------|-----------|
    |**名称**|**插入**|
    |**Text**|**插入**|

12. 调整用户控件的大小以适应控件。

## <a name="set-up-the-data-source"></a>设置数据源
 若要设置数据源，请将代码添加到 <xref:System.Windows.Forms.UserControl.Load> 操作窗格控件的事件中，以利用中的数据填充控件 <xref:System.Data.DataTable> ，并设置 <xref:System.Windows.Forms.Binding.DataSource%2A> <xref:System.Windows.Forms.BindingSource.DataMember%2A> 每个控件的和属性。

### <a name="to-load-the-control-with-data"></a>加载包含数据的控件

1. 在 <xref:System.Windows.Forms.UserControl.Load> 类的事件处理程序中 `ActionsControl` ，添加以下代码。

     [!code-vb[Trin_VstcoreActionsPaneWord#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb#1)]
     [!code-csharp[Trin_VstcoreActionsPaneWord#1](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#1)]

2. 在 c # 中，必须将事件处理程序附加到 <xref:System.Windows.Forms.UserControl.Load> 事件。 可以在调用后将此代码放在 `ActionsControl` 构造函数中 `InitializeComponent` 。 有关如何创建事件处理程序的详细信息，请参阅 [如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_VstcoreActionsPaneWord#33](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#33)]

### <a name="to-set-data-binding-properties-of-the-controls"></a>设置控件的数据绑定属性

1. 选择 `CompanyNameComboBox` 控件。

2. 在 " **属性** " 窗口中，单击 " **DataSource** " 属性右侧的按钮，然后选择 " **suppliersBindingSource**"。

3. 单击 " **DisplayMember** " 属性右侧的按钮，然后选择 " **公司名称**"。

4. 展开 "databinding **" 属性，** 单击 " **文本** " 属性右侧的按钮，然后选择 " **无**"。

5. 选择 `ProductNameListBox` 控件。

6. 在 " **属性** " 窗口中，单击 " **DataSource** " 属性右侧的按钮，然后选择 " **productsBindingSource**"。

7. 单击 " **DisplayMember** " 属性右侧的按钮，然后选择 " **ProductName**"。

8. 展开 "databinding **" 属性，** 单击 " **SelectedValue** " 属性右侧的按钮，然后选择 " **无**"。

## <a name="add-a-method-to-insert-data-into-a-table"></a>添加用于向表中插入数据的方法
 下一个任务是读取绑定控件中的数据，并在 Word 文档中填充一个表。 首先，创建一个用于设置表中标题格式的过程，然后添加 `AddData` 方法来创建 Word 表并设置其格式。

### <a name="to-format-the-table-headings"></a>设置表标题的格式

1. 在 `ActionsControl` 类中，创建一个用于设置表标题格式的方法。

     [!code-vb[Trin_VstcoreActionsPaneWord#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb#2)]
     [!code-csharp[Trin_VstcoreActionsPaneWord#2](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#2)]

### <a name="to-create-the-table"></a>创建表

1. 在 `ActionsControl` 类中，编写一个方法，该方法将创建表（如果该表尚不存在），并将操作窗格中的数据添加到表中。

     [!code-vb[Trin_VstcoreActionsPaneWord#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb#3)]
     [!code-csharp[Trin_VstcoreActionsPaneWord#3](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#3)]

### <a name="to-insert-text-into-a-word-table"></a>向 Word 表中插入文本

1. 将以下代码添加到 <xref:System.Windows.Forms.Control.Click> " **插入** " 按钮的事件处理程序中。

     [!code-vb[Trin_VstcoreActionsPaneWord#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb#4)]
     [!code-csharp[Trin_VstcoreActionsPaneWord#4](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#4)]

2. 在 c # 中，必须为按钮的事件创建事件处理程序 <xref:System.Windows.Forms.Control.Click> 。  可以将此代码放在 <xref:System.Windows.Forms.UserControl.Load> 类的事件处理程序中 `ActionsControl` 。

     [!code-csharp[Trin_VstcoreActionsPaneWord#5](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#5)]

## <a name="show-the-actions-pane"></a>显示操作窗格
 添加控件后，"操作" 窗格将变为可见。

### <a name="to-show-the-actions-pane"></a>显示操作窗格

1. 在 **解决方案资源管理器**中，右键单击 " **ThisDocument** " 或 " **ThisDocument.cs**"，然后单击快捷菜单上的 " **查看代码** "。

2. 在类的顶部创建控件的新实例， `ThisDocument` 使其类似于下面的示例。

     [!code-csharp[Trin_VstcoreActionsPaneWord#6](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#6)]
     [!code-vb[Trin_VstcoreActionsPaneWord#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#6)]

3. 将代码添加到 <xref:Microsoft.Office.Tools.Word.Document.Startup> 事件处理程序中， `ThisDocument` 以使其类似于下面的示例。

     [!code-csharp[Trin_VstcoreActionsPaneWord#7](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#7)]
     [!code-vb[Trin_VstcoreActionsPaneWord#7](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#7)]

## <a name="test-the-application"></a>测试应用程序
 现在，你可以对文档进行测试，以验证在打开文档时是否显示操作窗格。 在 "操作" 窗格上的控件中测试大纲/细节关系，并确保在单击 " **插入** " 按钮时，将数据填充到 Word 表中。

### <a name="to-test-your-document"></a>测试文档

1. 按 **F5** 运行项目。

2. 确认操作窗格可见。

3. 在组合框中选择一个公司，并验证 " **产品** " 列表框中的项是否更改。

4. 选择一个产品，单击 "操作" 窗格上的 " **插入** "，然后验证是否已将产品详细信息添加到 Word 的表中。

5. 插入来自各种公司的其他产品。

## <a name="next-steps"></a>后续步骤
 本演练演示如何将数据绑定到 Word 中操作窗格上的控件。 以下是接下来可能要执行的一些任务：

- 将数据绑定到 Excel 中的控件。 有关详细信息，请参阅 [演练：将数据绑定到 Excel 操作窗格上的控件](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md)。

- 部署项目。 有关详细信息，请参阅 [使用 ClickOnce 部署 Office 解决方案](../vsto/deploying-an-office-solution-by-using-clickonce.md)。

## <a name="see-also"></a>另请参阅
- [操作窗格概述](../vsto/actions-pane-overview.md)
- [如何：向 Word 文档或 Excel 工作簿添加操作窗格](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
