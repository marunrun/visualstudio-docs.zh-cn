---
title: 使用缓存的数据集创建主/从关系
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- master-detail tables [Office development in Visual Studio], walkthroughs
- data caching [Office development in Visual Studio], Master/Detail Relation
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0acf84dd983a8c10f2af526ae0bb904eaa90a360
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "67328353"
---
# <a name="walkthrough-create-a-master-detail-relation-using-a-cached-dataset"></a>演练：使用缓存的数据集创建主/从关系
  本演练演示如何在工作表上创建主/从关系以及缓存数据，以便可以脱机使用该解决方案。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 在本演练中，你将学会如何执行以下任务：

- 向工作表添加控件。

- 设置要在工作表中缓存的数据集。

- 添加代码以启用滚动记录。

- 测试项目。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- 访问 Northwind SQL Server 示例数据库。 数据库可以在开发计算机上，也可以在服务器上。

- 用于读取和写入 SQL Server 数据库的权限。

## <a name="create-a-new-project"></a>创建新项目
 在此步骤中，您将创建一个 Excel 工作簿项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 使用 Visual Basic 或 c # 创建一个名为 **Master-Detail**的 Excel 工作簿项目。 请确保已选中 " **创建新文档** "。 有关详细信息，请参阅 [How to: Create Office Projects in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)。

   Visual Studio 将在设计器中打开新的 Excel 工作簿，并将 **我的母版页-Detail** 项目添加到 **解决方案资源管理器**。

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

8. 选择 " **订单** " 表和 " **订单详细信息** " 表。

9. 单击“完成”。

   向导将两个表添加到 " **数据源** " 窗口。 它还将一个类型化数据集添加到你的项目中，该数据集在 **解决方案资源管理器**中可见。

## <a name="add-controls-to-the-worksheet"></a>向工作表添加控件
 在此步骤中，您将向第一个工作表添加命名范围、列表对象和两个按钮。 首先，从 " **数据源** " 窗口添加命名范围和列表对象，以便将其自动绑定到数据源。 接下来，从 " **工具箱**" 中添加按钮。

### <a name="to-add-a-named-range-and-a-list-object"></a>添加命名范围和列表对象

1. 验证是否在 Visual Studio 设计器中打开了 **"我的 Master-Detail.xlsx** 工作簿"，其中显示了 **Sheet1** 。

2. 打开 " **数据源** " 窗口并展开 " **Orders** " 节点。

3. 选择 " **订单 id** " 列，然后单击显示的下拉箭头。

4. 在下拉列表中单击 " **NamedRange** "，然后将 " **订单 id** " 列拖到单元格 **A2**。

     <xref:Microsoft.Office.Tools.Excel.NamedRange> `OrderIDNamedRange` 在单元**A2**中创建名为的控件。 同时，会将一个 <xref:System.Windows.Forms.BindingSource> 名为的 `OrdersBindingSource` 表适配器和一个 <xref:System.Data.DataSet> 实例添加到该项目中。 控件绑定到 <xref:System.Windows.Forms.BindingSource> ，而后者又绑定到该 <xref:System.Data.DataSet> 实例。

5. 向下滚动到 " **Orders** " 表下的列。 列表底部是 **Order Details** 表;这是因为它是 **Orders** 表的子表。 选择此 **订单详细信息** 表，而不是与 **Orders** 表处于同一级别的表，然后单击显示的下拉箭头。

6. 在下拉列表中单击 " **ListObject** "，然后将 " **OrderDetails** " 表拖到单元格 **A6**。

7. <xref:Microsoft.Office.Tools.Excel.ListObject>名为**Order_DetailsListObject**的控件在单元格**A6**中创建，并绑定到 <xref:System.Windows.Forms.BindingSource> 。

### <a name="to-add-two-buttons"></a>添加两个按钮

1. 从 "**工具箱**" 的 "**公共控件**" 选项卡中，将 <xref:System.Windows.Forms.Button> 控件添加到工作表的单元格**A3** 。

    此按钮的名称为 `Button1` 。

2. 向 <xref:System.Windows.Forms.Button> 工作表的单元格 **B3** 添加另一个控件。

    此按钮的名称为 `Button2` 。

   接下来，标记要缓存在文档中的数据集。

## <a name="cache-the-dataset"></a>缓存数据集
 通过使数据集公开并设置 **CacheInDocument** 属性，将数据集标记为在文档中进行缓存。

### <a name="to-cache-the-dataset"></a>缓存数据集

1. 在组件栏中选择 " **NorthwindDataSet** "。

2. 在 " **属性** " 窗口中，将 " **修饰符** " 属性更改为 " **公共**"。

    启用缓存之前，数据集必须是公共的。

3. 将 **CacheInDocument** 属性更改为 **True**。

   下一步是向按钮添加文本，并在 c # 中添加代码以挂接事件处理程序。

## <a name="initialize-the-controls"></a>初始化控件
 设置按钮文本，并在事件期间添加事件处理程序 <xref:Microsoft.Office.Tools.Excel.Workbook.Startup> 。

### <a name="to-initialize-the-data-and-the-controls"></a>初始化数据和控件

1. 在 **解决方案资源管理器**中，右键单击 " **Sheet1** " 或 " **Sheet1.cs**"，然后单击快捷菜单上的 " **查看代码** "。

2. 将以下代码添加到 `Sheet1_Startup` 方法以设置按钮的文本。

     [!code-vb[Trin_VstcoreDataExcel#15](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb#15)]
     [!code-csharp[Trin_VstcoreDataExcel#15](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs#15)]

3. 仅适用于 c #，将按钮单击事件的事件处理程序添加到 `Sheet1_Startup` 方法。

     [!code-csharp[Trin_VstcoreDataExcel#16](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs#16)]

## <a name="add-code-to-enable-scrolling-through-the-records"></a>添加代码以启用滚动记录
 将代码添加到 <xref:System.Windows.Forms.Control.Click> 每个按钮的事件处理程序，以在记录中移动。

### <a name="to-scroll-through-the-records"></a>滚动显示记录

1. 为的事件添加事件处理程序 <xref:System.Windows.Forms.Control.Click> `Button1` ，并添加以下代码以在记录中向后移动：

     [!code-vb[Trin_VstcoreDataExcel#17](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb#17)]
     [!code-csharp[Trin_VstcoreDataExcel#17](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs#17)]

2. 为的事件添加事件处理程序 <xref:System.Windows.Forms.Control.Click> `Button2` ，并添加以下代码以提前完成记录：

     [!code-vb[Trin_VstcoreDataExcel#18](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet2.vb#18)]
     [!code-csharp[Trin_VstcoreDataExcel#18](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet2.cs#18)]

## <a name="test-the-application"></a>测试应用程序
 现在，你可以测试工作簿以确保数据按预期方式显示，并且可以脱机使用该解决方案。

### <a name="to-test-the-data-caching"></a>测试数据缓存

1. 按 **F5**。

2. 验证命名范围和列表对象是否用数据源中的数据进行填充。

3. 单击按钮，滚动查看一些记录。

4. 保存工作簿，然后关闭工作簿和 Visual Studio。

5. 禁用与数据库的连接。 如果数据库位于服务器上，则从计算机拔下网线，如果数据库位于开发计算机上，则停止 SQL Server 服务。

6. 打开 "Excel"，然后从*\bin*目录中打开 **"我的 Master-Detail.xlsx** (*\My Master-Detail\bin* in c # ) 中的 Visual Basic 或*\My Master-Detail\bin\debug* 。

7. 滚动查看一些记录，查看在断开连接时工作表的运行是否正常。

8. 重新连接到数据库。 如果数据库位于服务器上，则再次将计算机连接到网络，如果数据库位于开发计算机上，则启动 SQL Server 服务。

## <a name="next-steps"></a>后续步骤
 本演练演示了在工作表上创建主/详细数据关系并缓存数据集的基本知识。 以下是接下来可能要执行的一些任务：

- 部署该解决方案。 有关详细信息，请参阅 [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)

## <a name="see-also"></a>另请参阅
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Office 解决方案中的数据](../vsto/data-in-office-solutions.md)
- [缓存数据](../vsto/caching-data.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
