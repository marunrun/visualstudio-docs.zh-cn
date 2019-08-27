---
title: 演练：在文档级项目中的简单数据绑定
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding [Office development in Visual Studio], worksheet cell to Database field
- worksheets [Office development in Visual Studio], binding worksheet cell to Database field
- Database field [Office development in Visual Studio]
- data [Office development in Visual Studio], binding data
- simple data binding [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f3b573842aee5f00f161213cf3e01dfcc4c8ba93
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62981057"
---
# <a name="walkthrough-simple-data-binding-in-a-document-level-project"></a>演练：在文档级项目中的简单数据绑定
  本演练演示在文档级项目中的数据绑定的基础知识。 SQL Server 数据库中的单个数据字段绑定到在 Microsoft Office Excel 中的命名区域。 本演练还演示如何添加控件，您可以滚动浏览表中的所有记录。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 本演练阐释了以下任务：

- 创建 Excel 项目的数据源。

- 将控件添加到工作表。

- 滚动查看数据库记录。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- 对具有 Northwind SQL Server 示例数据库的服务器的访问。

- 读取和写入到 SQL Server 数据库的权限。

## <a name="create-a-new-project"></a>创建新项目
 在此步骤中，将创建一个 Excel 工作簿项目。

### <a name="to-create-a-new-project"></a>创建新项目

1. 使用名称创建的 Excel 工作簿项目**我的简单数据绑定**，使用 Visual Basic 或 C#。 请确保**创建一个新文档**处于选中状态。 有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

   Visual Studio 设计器中打开新 Excel 工作簿并将添加**我的简单数据绑定**投影到**解决方案资源管理器**。

## <a name="create-the-data-source"></a>创建数据源
 使用 **“数据源”** 窗口将类型化数据集添加到项目中。

### <a name="to-create-the-data-source"></a>创建数据源

1. 如果**数据源**窗口不可见，显示它，在菜单栏中选择**视图** > **其他 Windows**  >  **数据源**。

2. 选择 **“添加新数据源”** 以启动 **“数据源配置向导”** 。

3. 选择**数据库**，然后单击**下一步**。

4. 选择数据连接到 Northwind 示例 SQL Server 数据库，或添加新的连接使用**新的连接**按钮。

5. 选择或创建连接后，单击**下一步**。

6. 如果选中，保存连接的选项，然后单击清除**下一步**。

7. 展开**表**中的节点**数据库对象**窗口。

8. 选中复选框旁边**客户**表。

9. 单击 **“完成”** 。

   该向导将添加**客户**表向**数据源**窗口。 它还将类型化数据集添加到项目中的可见**解决方案资源管理器**。

## <a name="add-controls-to-the-worksheet"></a>将控件添加到工作表
 对于本演练，你需要两个命名的范围和第一个工作表上的四个按钮。 首先，添加两个命名的范围是从**数据源**窗口，从而使它们自动绑定到数据源。 接下来，添加从按钮**工具箱**。

### <a name="to-add-two-named-ranges"></a>若要添加两个名为范围

1. 确认*我的简单数据 Binding.xlsx*工作簿是在 Visual Studio 设计器中，打开与**Sheet1**显示。

2. 打开**数据源**窗口中，展开**客户**节点。

3. 选择**CompanyName**列，然后单击显示的下拉箭头。

4. 选择**NamedRange**在下拉列表中，然后将**CompanyName**到单元格的列**A1**。

     一个<xref:Microsoft.Office.Tools.Excel.NamedRange>名为控件`companyNameNamedRange`单元格中创建**A1**。 同时，在<xref:System.Windows.Forms.BindingSource>名为`customersBindingSource`，一个表适配器和一个<xref:System.Data.DataSet>实例添加到项目。 该控件绑定到<xref:System.Windows.Forms.BindingSource>，后者又绑定到<xref:System.Data.DataSet>实例。

5. 选择**CustomerID**中的列**数据源**窗口中，然后单击显示的下拉箭头。

6. 单击**NamedRange**在下拉列表中，然后将**CustomerID**到单元格的列**B1**。

7. 另一个<xref:Microsoft.Office.Tools.Excel.NamedRange>名为控件`customerIDNamedRange`单元格中创建**B1**，并将其绑定到<xref:System.Windows.Forms.BindingSource>。

### <a name="to-add-four-buttons"></a>若要添加四个按钮

1. 从**公共控件**选项卡**工具箱**，添加<xref:System.Windows.Forms.Button>单元格的控件**A3**的工作表。

    此按钮名为`Button1`。

2. 将三个按钮添加到此顺序中的以下单元格，以使名称所示：

   |单元格|(名称)|
   |----------|--------------|
   |B3|Button2|
   |C3|Button3|
   |D3|Button4|

   下一步是将文本添加到按钮，并在 C# 中添加事件处理程序。

## <a name="initialize-the-controls"></a>初始化控件
 设置按钮文本和添加事件处理程序期间<xref:Microsoft.Office.Tools.Excel.Worksheet.Startup>事件。

### <a name="to-initialize-the-controls"></a>若要初始化控件

1. 在中**解决方案资源管理器**，右键单击**Sheet1.vb**或**Sheet1.cs**，然后单击**查看代码**快捷菜单上。

2. 将以下代码添加到`Sheet1_Startup`方法以设置每个按钮的文本。

    [!code-csharp[Trin_VstcoreDataExcel#2](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#2)]
    [!code-vb[Trin_VstcoreDataExcel#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#2)]

3. 仅适用于 C#，添加事件处理程序按钮的 click 事件与`Sheet1_Startup`方法。

    [!code-csharp[Trin_VstcoreDataExcel#3](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#3)]

   现在，添加代码来处理<xref:System.Windows.Forms.Control.Click>按钮的事件的以便用户可以浏览记录。

## <a name="add-code-to-enable-scrolling-through-the-records"></a>添加代码以启用滚动记录
 将代码添加到<xref:System.Windows.Forms.Control.Click>的每个按钮以浏览记录的事件处理程序。

### <a name="to-move-to-the-first-record"></a>若要将移动到第一条记录

1. 添加事件处理程序<xref:System.Windows.Forms.Control.Click>事件的`Button1`按钮，然后添加以下代码以将移动到第一条记录：

     [!code-csharp[Trin_VstcoreDataExcel#4](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#4)]
     [!code-vb[Trin_VstcoreDataExcel#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#4)]

### <a name="to-move-to-the-previous-record"></a>若要将移动到上一条记录

1. 添加事件处理程序<xref:System.Windows.Forms.Control.Click>事件的`Button2`按钮，然后添加以下代码以返回由一个移动的位置：

     [!code-csharp[Trin_VstcoreDataExcel#5](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#5)]
     [!code-vb[Trin_VstcoreDataExcel#5](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#5)]

### <a name="to-move-to-the-next-record"></a>若要将移动到下一条记录

1. 添加事件处理程序<xref:System.Windows.Forms.Control.Click>事件的`Button3`按钮，然后添加以下代码，以提升的一个位置：

     [!code-csharp[Trin_VstcoreDataExcel#6](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#6)]
     [!code-vb[Trin_VstcoreDataExcel#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#6)]

### <a name="to-move-to-the-last-record"></a>若要移动到最后一个记录

1. 添加事件处理程序<xref:System.Windows.Forms.Control.Click>事件的`Button4`按钮，然后添加以下代码以移动到最后一个记录：

     [!code-csharp[Trin_VstcoreDataExcel#7](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#7)]
     [!code-vb[Trin_VstcoreDataExcel#7](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#7)]

## <a name="test-the-application"></a>测试应用程序
 现在，你可以测试你的工作簿，以确保您可以浏览数据库中的记录。

### <a name="to-test-your-workbook"></a>测试工作簿

1. 按**F5**运行你的项目。

2. 确认第一条记录显示在单元格**A1**并**B1**。

3. 单击 **>** (`Button3`) 按钮，然后确认下一条记录显示在单元格中**A1**并**B1**。

4. 单击其他滚动按钮以确认该记录按预期发生变化。

## <a name="next-steps"></a>后续步骤
 本演练演示绑定到数据库中的字段的命名的范围的基础知识。 以下是接下来可能要执行的一些任务：

- 缓存数据，以便可以脱机使用。 有关详细信息，请参阅[如何：脱机时或者在服务器上缓存数据以供使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)。

- 将单元格到多个列在表中，而不是绑定到的一个字段。 有关详细信息，请参见[演练：在文档级项目中的复杂数据绑定](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)。

- 使用<xref:System.Windows.Forms.BindingNavigator>控件滚动显示记录。 有关详细信息，请参阅[如何：使用 Windows 窗体 BindingNavigator 控件导航数据](/dotnet/framework/winforms/controls/bindingnavigator-control-overview-windows-forms)。

## <a name="see-also"></a>请参阅
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Office 解决方案中的数据](../vsto/data-in-office-solutions.md)
- [演练：在文档级项目中的复杂数据绑定](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)
