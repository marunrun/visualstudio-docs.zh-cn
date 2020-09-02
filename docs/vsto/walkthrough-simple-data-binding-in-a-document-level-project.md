---
title: 演练：文档级项目中的简单数据绑定
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62981057"
---
# <a name="walkthrough-simple-data-binding-in-a-document-level-project"></a>演练：文档级项目中的简单数据绑定
  本演练演示了文档级项目中的数据绑定基础知识。 SQL Server 数据库中的单个数据字段绑定到 Microsoft Office Excel 中的命名范围。 本演练还演示如何添加控件，使您可以滚动浏览表中的所有记录。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 本演练演示以下任务：

- 为 Excel 项目创建数据源。

- 向工作表添加控件。

- 滚动查看数据库记录。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- 使用 Northwind SQL Server 示例数据库访问服务器。

- 用于读取和写入 SQL Server 数据库的权限。

## <a name="create-a-new-project"></a>创建新项目
 在此步骤中，您将创建一个 Excel 工作簿项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 使用 Visual Basic 或 c # 创建一个名为 **"我的简单数据绑定**" 的 Excel 工作簿项目。 请确保已选中 " **创建新文档** "。 有关详细信息，请参阅 [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

   Visual Studio 将在设计器中打开新的 Excel 工作簿，并将 **我的简单数据绑定** 项目添加到 **解决方案资源管理器**。

## <a name="create-the-data-source"></a>创建数据源
 使用 **“数据源”** 窗口将类型化数据集添加到项目中。

### <a name="to-create-the-data-source"></a>创建数据源

1. 如果 "**数据源**" 窗口不可见，请在菜单栏上选择 "**查看**  >  **其他 Windows**  >  **数据源**"，将其显示出来。

2. 选择 **“添加新数据源”** 以启动 **“数据源配置向导”**。

3. 选择 **数据库** ，然后单击 " **下一步**"。

4. 选择与 Northwind 示例 SQL Server 数据库的数据连接，或使用 " **新建连接** " 按钮添加新连接。

5. 选择或创建连接后，单击 " **下一步**"。

6. 清除 "保存连接" 选项，然后单击 " **下一步**"。

7. 展开 "**数据库对象**" 窗口中的 "**表**" 节点。

8. 选中 " **Customers** " 表旁边的复选框。

9. 单击“完成”。

   向导会将 **Customers** 表添加到 " **数据源** " 窗口。 它还将一个类型化数据集添加到你的项目中，该数据集在 **解决方案资源管理器**中可见。

## <a name="add-controls-to-the-worksheet"></a>向工作表添加控件
 对于本演练，您需要在第一个工作表上有两个命名范围和四个按钮。 首先，从 " **数据源** " 窗口添加两个命名范围，以便它们自动绑定到数据源。 接下来，从 " **工具箱**" 中添加按钮。

### <a name="to-add-two-named-ranges"></a>添加两个命名范围

1. 验证是否在 Visual Studio 设计器中打开了 " *我的简单数据 Binding.xlsx* 工作簿"，其中显示了 **Sheet1** 。

2. 打开 " **数据源** " 窗口并展开 " **Customers** " 节点。

3. 选择 " **公司名称** " 列，然后单击显示的下拉箭头。

4. 在下拉列表中选择 " **NamedRange** "，然后将 " **公司名称** " 列拖到单元格 **A1**。

     <xref:Microsoft.Office.Tools.Excel.NamedRange> `companyNameNamedRange` 在单元格**A1**中创建一个名为的控件。 同时，会将一个 <xref:System.Windows.Forms.BindingSource> 名为的 `customersBindingSource` 表适配器和一个 <xref:System.Data.DataSet> 实例添加到该项目中。 控件绑定到 <xref:System.Windows.Forms.BindingSource> ，而后者又绑定到该 <xref:System.Data.DataSet> 实例。

5. 在 "**数据源**" 窗口中选择 " **CustomerID** " 列，然后单击显示的下拉箭头。

6. 在下拉列表中单击 " **NamedRange** "，然后将 " **CustomerID** " 列拖到单元格 **B1**。

7. 名为的另一个 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件 `customerIDNamedRange` 在单元格 **B1**中创建，并绑定到 <xref:System.Windows.Forms.BindingSource> 。

### <a name="to-add-four-buttons"></a>添加四个按钮

1. 从 "**工具箱**" 的 "**公共控件**" 选项卡中，将 <xref:System.Windows.Forms.Button> 控件添加到工作表的单元格**A3** 。

    此按钮的名称为 `Button1` 。

2. 按此顺序向以下单元格添加另外三个按钮，使名称如下所示：

   |单元|(名称)|
   |----------|--------------|
   |B3|Button2|
   |C3|Button3|
   |D3|Button4|

   下一步是向按钮添加文本，并在 c # 中添加事件处理程序。

## <a name="initialize-the-controls"></a>初始化控件
 设置按钮文本，并在事件期间添加事件处理程序 <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> 。

### <a name="to-initialize-the-controls"></a>初始化控件

1. 在 **解决方案资源管理器**中，右键单击 " **Sheet1** " 或 " **Sheet1.cs**"，然后单击快捷菜单上的 " **查看代码** "。

2. 将以下代码添加到 `Sheet1_Startup` 方法以设置每个按钮的文本。

    [!code-csharp[Trin_VstcoreDataExcel#2](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#2)]
    [!code-vb[Trin_VstcoreDataExcel#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#2)]

3. 仅适用于 c #，将按钮单击事件的事件处理程序添加到 `Sheet1_Startup` 方法。

    [!code-csharp[Trin_VstcoreDataExcel#3](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#3)]

   现在添加代码以处理 <xref:System.Windows.Forms.Control.Click> 按钮的事件，使用户可以浏览记录。

## <a name="add-code-to-enable-scrolling-through-the-records"></a>添加代码以启用滚动记录
 将代码添加到 <xref:System.Windows.Forms.Control.Click> 每个按钮的事件处理程序，以在记录中移动。

### <a name="to-move-to-the-first-record"></a>移动到第一条记录

1. 为按钮的事件添加事件处理程序 <xref:System.Windows.Forms.Control.Click> `Button1` ，并添加以下代码以移动到第一条记录：

     [!code-csharp[Trin_VstcoreDataExcel#4](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#4)]
     [!code-vb[Trin_VstcoreDataExcel#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#4)]

### <a name="to-move-to-the-previous-record"></a>移动到上一条记录

1. 为按钮的事件添加事件处理程序 <xref:System.Windows.Forms.Control.Click> `Button2` ，并添加以下代码以将位置向后移动一个：

     [!code-csharp[Trin_VstcoreDataExcel#5](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#5)]
     [!code-vb[Trin_VstcoreDataExcel#5](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#5)]

### <a name="to-move-to-the-next-record"></a>移到下一条记录

1. 为按钮的事件添加事件处理程序 <xref:System.Windows.Forms.Control.Click> `Button3` ，并添加以下代码以将位置前移一：

     [!code-csharp[Trin_VstcoreDataExcel#6](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#6)]
     [!code-vb[Trin_VstcoreDataExcel#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#6)]

### <a name="to-move-to-the-last-record"></a>移到最后一条记录

1. 为按钮的事件添加事件处理程序 <xref:System.Windows.Forms.Control.Click> `Button4` ，并添加以下代码以移动到最后一条记录：

     [!code-csharp[Trin_VstcoreDataExcel#7](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#7)]
     [!code-vb[Trin_VstcoreDataExcel#7](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#7)]

## <a name="test-the-application"></a>测试应用程序
 现在可以测试工作簿，以确保可以浏览数据库中的记录。

### <a name="to-test-your-workbook"></a>测试工作簿

1. 按 **F5** 运行项目。

2. 确认第一条记录显示在单元格 **A1** 和 **B1**中。

3. 单击 " **>** (`Button3`) " 按钮，确认下一条记录显示在单元格 **A1** 和 **B1**中。

4. 单击其他滚动按钮以确认记录是否按预期方式发生更改。

## <a name="next-steps"></a>后续步骤
 此演练演示将命名范围绑定到数据库中的字段的基础知识。 以下是接下来可能要执行的一些任务：

- 缓存数据，以便可以脱机使用。 有关详细信息，请参阅 [如何：缓存数据以便脱机使用或在服务器上使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)。

- 将单元格绑定到表中的多个列，而不是绑定到一个字段。 有关详细信息，请参阅 [演练：文档级项目中的复杂数据绑定](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)。

- 使用 <xref:System.Windows.Forms.BindingNavigator> 控件滚动记录。 有关详细信息，请参阅 [如何：用 Windows 窗体 BindingNavigator 控件浏览数据](/dotnet/framework/winforms/controls/bindingnavigator-control-overview-windows-forms)。

## <a name="see-also"></a>另请参阅
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Office 解决方案中的数据](../vsto/data-in-office-solutions.md)
- [演练：文档级项目中的复杂数据绑定](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)
