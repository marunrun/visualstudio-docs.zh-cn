---
title: 演练：将数据绑定到 Excel 操作窗格上的控件
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
ms.openlocfilehash: 1543f872961d556674dd5ad6b3f5b8071d2d404b
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71253884"
---
# <a name="walkthrough-bind-data-to-controls-on-an-excel-actions-pane"></a>演练：将数据绑定到 Excel 操作窗格上的控件
  本演练演示如何将数据绑定到 Microsoft Office Excel 中操作窗格上的控件。 控件演示 SQL Server 数据库中表之间的主/从关系。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 本演练阐释了以下任务：

- 向工作表添加控件。

- 创建操作窗格控件。

- 向操作窗格控件添加数据绑定 Windows 窗体控件。

- 当应用程序打开时显示操作窗格。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- 使用 Northwind SQL Server 示例数据库访问服务器。

- 用于读取和写入 SQL Server 数据库的权限。

## <a name="create-the-project"></a>创建项目
 第一步是创建一个 Excel 工作簿项目。

### <a name="to-create-a-new-project"></a>创建新项目

1. 使用 "**我的 Excel 操作" 窗格**创建一个 Excel 工作簿项目。 在向导中，选择 "**创建新文档**"。 有关详细信息，请参阅[如何：在 Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)中创建 Office 项目。

     Visual Studio 将在设计器中打开新的 Excel 工作簿，并将 "**我的 Excel 操作" 窗格**项目添加到**解决方案资源管理器**。

## <a name="add-a-new-data-source-to-the-project"></a>向项目中添加新的数据源

### <a name="to-add-a-new-data-source-to-the-project"></a>向项目中添加新的数据源

1. 如果 "**数据源**" 窗口不可见，请在菜单栏上选择 "**查看** > **其他 Windows** > **数据源**"，将其显示出来。

2. 选择 **“添加新数据源”** 以启动 **“数据源配置向导”** 。

3. 选择**数据库**，然后单击 "**下一步**"。

4. 选择与 Northwind 示例 SQL Server 数据库的数据连接，或使用 "**新建连接**" 按钮添加新连接。

5. 单击 **“下一步”** 。

6. 清除该选项以保存连接（如果已选中），然后单击 "**下一步**"。

7. 展开 "**数据库对象**" 窗口中的 "**表**" 节点。

8. 选中 "**供应商**" 表旁边的复选框。

9. 展开**Products**表，并选择 " **ProductName**"、"**供应商**"、" **QuantityPerUnit**" 和 "**单价**"。

10. 单击 **“完成”** 。

    向导将 "**供应商**表和**产品**" 表添加到 "**数据源**" 窗口。 它还将一个类型化数据集添加到你的项目中，该数据集在**解决方案资源管理器**中可见。

## <a name="add-controls-to-the-worksheet"></a>向工作表添加控件
 接下来，将<xref:Microsoft.Office.Tools.Excel.NamedRange>一个控件和<xref:Microsoft.Office.Tools.Excel.ListObject>一个控件添加到第一个工作表。

### <a name="to-add-a-namedrange-control-and-a-listobject-control"></a>添加 NamedRange 控件和 ListObject 控件

1. 验证是否已在 Visual Studio 设计器中打开 "**我的 Excel 操作" 窗格 .xlsx**工作`Sheet1`簿，并显示。

2. 在 "**数据源**" 窗口中，展开 "**供应商**" 表。

3. 单击 "**公司名称**" 节点上的下拉箭头，然后单击 " **NamedRange**"。

4. 将**公司名称**从 "**数据源**" 窗口拖到中`Sheet1`的单元格 A2。

     将<xref:Microsoft.Office.Tools.Excel.NamedRange> `CompanyNameNamedRange` **创建一个**名为的控件，并在单元格 A2 中显示 "公司名称">。\< 同时，将一个<xref:System.Windows.Forms.BindingSource>名为`suppliersBindingSource`的、一个<xref:System.Data.DataSet>表适配器和添加到该项目中。 控件绑定到<xref:System.Windows.Forms.BindingSource>，而后者又绑定<xref:System.Data.DataSet>到该实例。

5. 在 "**数据源**" 窗口中，向下滚动到 "**供应商**" 表下的列。 列表底部是**Products**表;因为它是 "**供应商**" 表的子站点。 选择 "此**产品**" 表，而不是与**供应商**表处于同一级别的表，然后单击显示的下拉箭头。

6. 在下拉列表中单击 " **ListObject** "，然后将**Products**表拖到中`Sheet1`的单元格**A6** 。

     在<xref:Microsoft.Office.Tools.Excel.ListObject>单元格`ProductNameListObject` **A6**中创建了一个名为的控件。 同时，会向项目中<xref:System.Windows.Forms.BindingSource>添加`productsBindingSource`一个名为的和一个表适配器。 控件绑定到<xref:System.Windows.Forms.BindingSource>，而后者又绑定<xref:System.Data.DataSet>到该实例。

7. 仅C#对于，在组件栏上选择**suppliersBindingSource** ，然后在 "**属性**" 窗口中将 "**修饰符**" 属性更改为 "**内部**"。

## <a name="add-controls-to-the-actions-pane"></a>向操作窗格添加控件
 接下来，需要一个包含组合框的操作窗格控件。

### <a name="to-add-an-actions-pane-control"></a>添加操作窗格控件

1. 在**解决方案资源管理器**中选择 "**我的 Excel 操作窗格**" 项目。

2. 在 **“项目”** 菜单上，单击 **“添加新项”** 。

3. 在 "**添加新项**" 对话框中，选择 "**操作窗格控件**"，将其命名为**ActionsControl**，然后单击 "**添加**"。

### <a name="to-add-data-bound-windows-forms-controls-to-an-actions-pane-control"></a>向操作窗格控件添加数据绑定 Windows 窗体控件

1. 从 "**工具箱**" 的 "**公共控件**" 选项卡<xref:System.Windows.Forms.ComboBox>中，将控件拖动到 "操作" 窗格控件。

2. 将 " **Size** " 属性更改为**171，21**。

3. 调整用户控件的大小以适合组合框。

## <a name="bind-the-control-on-the-actions-pane-to-data"></a>将操作窗格上的控件绑定到数据
 在本节中，您将把的<xref:System.Windows.Forms.ComboBox>数据源设置为与工作表上的<xref:Microsoft.Office.Tools.Excel.NamedRange>控件相同的数据源。

### <a name="to-set-data-binding-properties-of-the-control"></a>设置控件的数据绑定属性

1. 右键单击 "操作" 窗格控件，然后单击 "**查看代码**"。

2. 将下面的代码添加到<xref:System.Windows.Forms.UserControl.Load>操作窗格控件的事件中。

     [!code-vb[Trin_VstcoreActionsPaneExcel#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ActionsControl.vb#1)]
     [!code-csharp[Trin_VstcoreActionsPaneExcel#1](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ActionsControl.cs#1)]

3. 在C#中，必须为`ActionsControl`创建事件处理程序。 可以将此代码放在`ActionsControl`构造函数中。 有关创建事件处理程序的详细信息， [请参阅如何：在 Office 项目](../vsto/how-to-create-event-handlers-in-office-projects.md)中创建事件处理程序。

     [!code-csharp[Trin_VstcoreActionsPaneExcel#2](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ActionsControl.cs#2)]

## <a name="show-the-actions-pane"></a>显示操作窗格
 在运行时添加控件之前，操作窗格不可见。

#### <a name="to-show-the-actions-pane"></a>显示操作窗格

1. 在**解决方案资源管理器**中，右键单击 " *ThisWorkbook* " 或 " *ThisWorkbook.cs*"，然后单击 "**查看代码**"。

2. 在`ThisWorkbook`类中创建用户控件的新实例。

     [!code-csharp[Trin_VstcoreActionsPaneExcel#3](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs#3)]
     [!code-vb[Trin_VstcoreActionsPaneExcel#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb#3)]

3. 在的`ThisWorkbook`事件处理程序中，将控件添加到 "操作" 窗格中。 <xref:Microsoft.Office.Tools.Excel.Workbook.Startup>

     [!code-csharp[Trin_VstcoreActionsPaneExcel#4](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs#4)]
     [!code-vb[Trin_VstcoreActionsPaneExcel#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb#4)]

## <a name="test-the-application"></a>测试应用程序
 现在，你可以测试文档以验证在打开文档时操作窗格是否打开，以及控件是否具有主/从关系。

### <a name="to-test-your-document"></a>测试文档

1. 按**F5**运行项目。

2. 确认操作窗格可见。

3. 在列表框中选择一个公司。 验证<xref:Microsoft.Office.Tools.Excel.NamedRange>控件中是否列出了公司名称，以及<xref:Microsoft.Office.Tools.Excel.ListObject>控件中是否列出了产品详细信息。

4. 选择各种公司来验证公司名称和产品详细信息是否根据需要进行更改。

## <a name="next-steps"></a>后续步骤
 以下是接下来可能要执行的一些任务：

- 将数据绑定到 Word 中的控件。 有关详细信息，请参见[演练：将数据绑定到 Word 操作窗格](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md)上的控件。

- 部署项目。 有关详细信息，请参阅[使用 ClickOnce 部署 Office 解决方案](../vsto/deploying-an-office-solution-by-using-clickonce.md)。

## <a name="see-also"></a>请参阅
- [操作窗格概述](../vsto/actions-pane-overview.md)
- [如何：管理操作窗格上的控件布局](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
