---
title: 演练：文档级项目中的复杂数据绑定
description: 了解如何将 Microsoft Excel 工作表中的多个单元格绑定到 Northwind SQL Server 数据库中的字段。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], binding data
- complex data [Office development in Visual Studio]
- multiple column data binding [Office development in Visual Studio]
- data binding [Office development in Visual Studio], multiple columns
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 988394595e8aa4710a22e1fedf22a921481c7396
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97527111"
---
# <a name="walkthrough-complex-data-binding-in-a-document-level-project"></a>演练：文档级项目中的复杂数据绑定
  本演练演示文档级项目中的复杂数据绑定的基本知识。 可以将 Microsoft Office Excel 工作表中的多个单元格绑定到 Northwind SQL Server 数据库中的字段。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 本演练演示以下任务：

- 向工作簿项目添加数据源。

- 向工作表中添加数据绑定控件。

- 将数据更改保存回数据库。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- 使用 Northwind SQL Server 示例数据库访问服务器。

- 用于读取和写入 SQL Server 数据库的权限。

## <a name="create-a-new-project"></a>创建新项目
 第一步是创建一个 Excel 工作簿项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 创建一个名为 **"我的复杂数据绑定**" 的 Excel 工作簿项目。 在向导中，选择 " **创建新文档**"。

     有关详细信息，请参阅 [How to: Create Office Projects in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 将在设计器中打开新的 Excel 工作簿，并将 **我的复杂数据绑定** 项目添加到 **解决方案资源管理器**。

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

8. 选中 " **Employees** " 表旁边的复选框。

9. 单击“完成”。

   向导将 " **Employees** " 表添加到 " **数据源** " 窗口。 它还将一个类型化数据集添加到你的项目中，该数据集在 **解决方案资源管理器** 中可见。

## <a name="add-controls-to-the-worksheet"></a>向工作表添加控件
 打开工作簿时，工作表将显示 **Employees** 表。 用户可以对数据进行更改，然后通过单击按钮将这些更改保存回数据库。

 若要将工作表自动绑定到表，您可以 <xref:Microsoft.Office.Tools.Excel.ListObject> 从 " **数据源** " 窗口将控件添加到工作表中。 若要为用户授予保存更改的选项，请 <xref:System.Windows.Forms.Button> 从 " **工具箱**" 中添加一个控件。

#### <a name="to-add-a-list-object"></a>添加 list 对象

1. 验证是否在 Visual Studio 设计器中打开了 " **我的复杂数据 Binding.xlsx** 工作簿"，其中显示了 **Sheet1** 。

2. 打开 " **数据源** " 窗口并选择 " **员工** " 节点。

3. 单击显示的下拉箭头。

4. 在下拉列表中选择 " **ListObject** "。

5. 将 **Employees** 表拖到单元格 **A6**。

     <xref:Microsoft.Office.Tools.Excel.ListObject> `EmployeesListObject` 在单元格 **A6** 中创建了一个名为的控件。 同时，会将一个 <xref:System.Windows.Forms.BindingSource> 名为的 `EmployeesBindingSource` 表适配器和一个 <xref:System.Data.DataSet> 实例添加到该项目中。 控件绑定到 <xref:System.Windows.Forms.BindingSource> ，而后者又绑定到该 <xref:System.Data.DataSet> 实例。

### <a name="to-add-a-button"></a>添加按钮

1. 从 "**工具箱**" 的 "**公共控件**" 选项卡中，将 <xref:System.Windows.Forms.Button> 控件添加到工作表的单元格 **A4** 。

   下一步是在工作表打开时向按钮添加文本。

## <a name="initialize-the-control"></a>初始化控件
 向事件处理程序中的按钮添加文本 <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> 。

### <a name="to-initialize-the-control"></a>初始化控件

1. 在 **解决方案资源管理器** 中，右键单击 " **Sheet1** " 或 " **Sheet1.cs**"，然后单击快捷菜单上的 " **查看代码** "。

2. 将以下代码添加到 `Sheet1_Startup` 方法以设置 b 的文本 `utton` 。

    [!code-csharp[Trin_VstcoreDataExcel#8](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet3.cs#8)]
    [!code-vb[Trin_VstcoreDataExcel#8](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet3.vb#8)]

3. 仅适用于 c #，将事件的事件处理程序添加 <xref:System.Windows.Forms.Control.Click> 到 `Sheet1_Startup` 方法。

    [!code-csharp[Trin_VstcoreDataExcel#9](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet3.cs#9)]

   现在添加代码以处理 <xref:System.Windows.Forms.Control.Click> 按钮的事件。

## <a name="save-changes-to-the-database"></a>保存对数据库所做的更改
 对数据所做的任何更改只存在于本地数据集中，直到它们显式保存回数据库。

### <a name="to-save-changes-to-the-database"></a>保存对数据库所做的更改

1. 为的事件添加事件处理程序 <xref:System.Windows.Forms.Control.Click> `button` ，并添加以下代码以将数据集中所做的所有更改提交回数据库。

     [!code-csharp[Trin_VstcoreDataExcel#10](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet3.cs#10)]
     [!code-vb[Trin_VstcoreDataExcel#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet3.vb#10)]

## <a name="test-the-application"></a>测试应用程序
 现在，你可以测试工作簿以验证数据是否按预期方式显示，并且可以操作列表对象中的数据。

### <a name="to-test-the-data-binding"></a>测试数据绑定

- 按 F5 。

     验证在打开工作簿时，列表对象是否用 **Employees** 表中的数据进行填充。

### <a name="to-modify-data"></a>修改数据

1. 单击应包含名称 **李小明** 的单元格 **B7**。

2. 键入名称 **Anderson**，然后按 **enter**。

### <a name="to-modify-a-column-header"></a>修改列标题

1. 单击包含列标题 **LastName** 的单元格。

2. 键入 " **姓氏**"，其中包含两个单词之间的空格，然后按 **enter**。

### <a name="to-save-data"></a>保存数据

1. 单击工作表上的 " **保存** "。

2. 退出 Excel。 出现提示时，请单击 " **否** " 以保存所做的更改。

3. 按 **F5** 再次运行该项目。

     列表对象用 **Employees** 表中的数据进行填充。

4. 请注意，单元格 **B7** 中的名称仍为 **Anderson**，这是您所做的数据更改并保存回数据库。 因为列标题未绑定到数据库，并且您没有保存对工作表所做的更改，所以列标题 **LastName** 已改回其原始形式。

### <a name="to-add-new-rows"></a>添加新行

1. 选择列表对象内的单元格。

    新行显示在列表的底部， *\** 在新行的第一个单元格中，星号 ( * _) 。

2. 在空行中添加以下信息。

   |EmployeeID|LastName|FirstName|Title|
   |----------------|--------------|---------------|-----------|
   |10|Ito|Shu|销售经理|

### <a name="to-delete-rows"></a>删除行

- 右键单击工作表最左侧第16行 (第16行) ，然后单击 "_" "删除"。

### <a name="to-sort-the-rows-in-the-list"></a>对列表中的行进行排序

1. 选择列表内的单元格。

     箭头按钮显示在每个列标题中。

2. 单击 " **姓氏** " 列标题中的箭头按钮。

3. 单击 " **升序排序**"。

     行按姓氏的字母顺序排序。

### <a name="to-filter-information"></a>筛选信息

1. 选择列表内的单元格。

2. 单击 " **标题** " 列标题中的箭头按钮。

3. 单击 " **销售代表**"。

     此列表仅显示在 "**标题**" 列中有 **销售代表** 的那些行。

4. 再次单击 " **标题** " 列标题中的箭头按钮。

5. 单击 " **(所有)**"。

     删除筛选并显示所有行。

## <a name="next-steps"></a>后续步骤
 本演练演示将数据库中的表绑定到列表对象的基本知识。 以下是接下来可能要执行的一些任务：

- 缓存数据，以便可以脱机使用。 有关详细信息，请参阅 [如何：缓存数据以便脱机使用或在服务器上使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)。

- 部署该解决方案。 有关详细信息，请参阅 [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)。

- 创建字段和表之间的主/从关系。 有关详细信息，请参阅 [演练：使用缓存的数据集创建主/从关系](../vsto/walkthrough-creating-a-master-detail-relation-using-a-cached-dataset.md)。

## <a name="see-also"></a>另请参阅
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Office 解决方案中的数据](../vsto/data-in-office-solutions.md)
- [演练：文档级项目中的简单数据绑定](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md)
