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
ms.openlocfilehash: 5882f81eefb55bb0dc4451b8ffa43c2acfbf1df5
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438678"
---
# <a name="walkthrough-bind-data-to-controls-on-an-excel-actions-pane"></a>演练：将数据绑定到 Excel 操作窗格上的控件
  本演练演示了数据绑定到 Microsoft Office Excel 中的操作窗格上的控件。 控件演示 SQL Server 数据库中表之间的主/从关系。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 本演练阐释了以下任务：

- 将控件添加到工作表。

- 创建操作窗格控件。

- 将数据绑定 Windows 窗体控件添加到操作窗格控件。

- 当应用程序打开时显示操作窗格。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- 对具有 Northwind SQL Server 示例数据库的服务器的访问。

- 读取和写入到 SQL Server 数据库的权限。

## <a name="create-the-project"></a>创建项目
 第一步是创建一个 Excel 工作簿项目。

### <a name="to-create-a-new-project"></a>创建新项目

1. 使用名称创建的 Excel 工作簿项目**我的 Excel 操作窗格**。 在向导中，选择**创建一个新文档**。 有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 设计器中打开新 Excel 工作簿并将添加**我的 Excel 操作窗格**投影到**解决方案资源管理器**。

## <a name="add-a-new-data-source-to-the-project"></a>将新的数据源添加到项目

### <a name="to-add-a-new-data-source-to-the-project"></a>若要将新的数据源添加到项目

1. 如果**数据源**窗口不可见，显示它，在菜单栏中选择**视图** > **其他 Windows**  >  **数据源**。

2. 选择 **“添加新数据源”** 以启动 **“数据源配置向导”**。

3. 选择**数据库**，然后单击**下一步**。

4. 选择与 Northwind 示例 SQL Server 数据库的数据连接或通过添加新的连接**新的连接**按钮。

5. 单击 **“下一步”**。

6. 如果选中，保存连接的选项，然后单击清除**下一步**。

7. 展开**表**中的节点**数据库对象**窗口。

8. 选中复选框旁边**供应商**表。

9. 展开**产品**表，然后选择**ProductName**， **SupplierID**， **QuantityPerUnit**，和**UnitPrice**.

10. 单击 **“完成”**。

    该向导将添加**供应商**表和**产品**表**数据源**窗口。 它还将类型化数据集添加到项目中的可见**解决方案资源管理器**。

## <a name="add-controls-to-the-worksheet"></a>将控件添加到工作表
 接下来，添加<xref:Microsoft.Office.Tools.Excel.NamedRange>控件和一个<xref:Microsoft.Office.Tools.Excel.ListObject>到第一个工作表的控件。

### <a name="to-add-a-namedrange-control-and-a-listobject-control"></a>若要添加 NamedRange 控件和 ListObject 控件

1. 确认**我的 Excel 操作 Pane.xlsx**工作簿是在 Visual Studio 设计器中，打开与`Sheet1`显示。

2. 在中**数据源**窗口中，展开**供应商**表。

3. 单击下拉箭头**公司名称**节点，并单击**NamedRange**。

4. 拖动**公司名称**从**数据源**窗口中的对单元格**A2**中`Sheet1`。

     一个<xref:Microsoft.Office.Tools.Excel.NamedRange>名为控件`CompanyNameNamedRange`创建和文本\<公司名称 > 单元中将出现**A2**。 同时，在<xref:System.Windows.Forms.BindingSource>名为`suppliersBindingSource`，一个表适配器和一个<xref:System.Data.DataSet>添加到项目。 该控件绑定到<xref:System.Windows.Forms.BindingSource>，后者又绑定到<xref:System.Data.DataSet>实例。

5. 在中**数据源**窗口中，以前的专栏下的向下滚动**供应商**表。 在列表的底部**产品**表; 此处是因为它的子级**供应商**表。 选择此选项**产品**表，不是与同一级别的那个**供应商**表，并单击显示的下拉箭头。

6. 单击**ListObject**在下拉列表中，然后将**产品**表与单元格**A6**中`Sheet1`。

     一个<xref:Microsoft.Office.Tools.Excel.ListObject>名为控件`ProductNameListObject`单元格中创建**A6**。 同时，在<xref:System.Windows.Forms.BindingSource>名为`productsBindingSource`和表适配器添加到项目。 该控件绑定到<xref:System.Windows.Forms.BindingSource>，后者又绑定到<xref:System.Data.DataSet>实例。

7. 有关C#，选择**suppliersBindingSource**在组件栏中，并更改**修饰符**属性设置为**内部**中**属性**窗口。

## <a name="add-controls-to-the-actions-pane"></a>将控件添加到操作窗格
 接下来，需要一个具有组合框的操作窗格控件。

### <a name="to-add-an-actions-pane-control"></a>若要添加操作窗格控件

1. 选择**我的 Excel 操作窗格**项目中**解决方案资源管理器**。

2. 在 **“项目”** 菜单上，单击 **“添加新项”**。

3. 在中**添加新项**对话框中，选择**操作窗格控件**，其命名为**ActionsControl**，然后单击**添加**。

### <a name="to-add-data-bound-windows-forms-controls-to-an-actions-pane-control"></a>若要将数据绑定 Windows 窗体控件添加到操作窗格控件

1. 从**公共控件**选项卡**工具箱**，拖动<xref:System.Windows.Forms.ComboBox>到操作窗格控件的控件。

2. 更改**大小**属性设置为**171，21**。

3. 调整大小以适应组合框的用户控件。

## <a name="bind-the-control-on-the-actions-pane-to-data"></a>将操作窗格上的控件绑定到数据
 在本部分中，您将设置的数据源<xref:System.Windows.Forms.ComboBox>到同一数据源作为<xref:Microsoft.Office.Tools.Excel.NamedRange>工作表上的控件。

### <a name="to-set-data-binding-properties-of-the-control"></a>若要设置控件的数据绑定属性

1. 右键单击操作窗格控件，然后依次**查看代码**。

2. 将以下代码添加到<xref:System.Windows.Forms.UserControl.Load>操作窗格控件的事件。

     [!code-vb[Trin_VstcoreActionsPaneExcel#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ActionsControl.vb#1)]
     [!code-csharp[Trin_VstcoreActionsPaneExcel#1](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ActionsControl.cs#1)]

3. 在C#，必须创建的事件处理程序`ActionsControl`。 您可以将此代码放置在`ActionsControl`构造函数。 有关创建事件处理程序的详细信息，请参阅[如何：Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     [!code-csharp[Trin_VstcoreActionsPaneExcel#2](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ActionsControl.cs#2)]

## <a name="show-the-actions-pane"></a>显示操作窗格
 操作窗格不可见，直到在运行时添加控件。

#### <a name="to-show-the-actions-pane"></a>若要显示操作窗格

1. 在中**解决方案资源管理器**，右键单击*ThisWorkbook.vb*或*ThisWorkbook.cs*，然后单击**查看代码**。

2. 创建用户控件中的新实例`ThisWorkbook`类。

     [!code-csharp[Trin_VstcoreActionsPaneExcel#3](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs#3)]
     [!code-vb[Trin_VstcoreActionsPaneExcel#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb#3)]

3. 在中<xref:Microsoft.Office.Tools.Excel.Workbook.Startup>事件处理程序`ThisWorkbook`，将控件添加到操作窗格。

     [!code-csharp[Trin_VstcoreActionsPaneExcel#4](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs#4)]
     [!code-vb[Trin_VstcoreActionsPaneExcel#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb#4)]

## <a name="test-the-application"></a>测试应用程序
 现在可以测试文档，以验证操作窗格打开时打开文档，并且控件具有主/从关系。

### <a name="to-test-your-document"></a>测试文档

1. 按**F5**运行你的项目。

2. 确认操作窗格可见。

3. 在列表框中选择一家公司。 验证公司名称列在<xref:Microsoft.Office.Tools.Excel.NamedRange>控制和产品详细信息所示<xref:Microsoft.Office.Tools.Excel.ListObject>控件。

4. 选择不同的公司，若要验证的公司名称和适当的产品详细信息的更改。

## <a name="next-steps"></a>后续步骤
 以下是接下来可能要执行的一些任务：

- 数据绑定到 Word 中的控件。 有关详细信息，请参见[演练：将数据绑定到 Word 操作窗格上的控件](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md)。

- 部署项目。 有关详细信息，请参阅[通过使用 ClickOnce 部署 Office 解决方案](../vsto/deploying-an-office-solution-by-using-clickonce.md)。

## <a name="see-also"></a>请参阅
- [操作窗格概述](../vsto/actions-pane-overview.md)
- [如何：管理操作窗格上的控件布局](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
