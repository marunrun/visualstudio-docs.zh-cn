---
title: 演练：将数据插入到服务器上的工作簿
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- datasets [Office development in Visual Studio], accessing on server
- server-side data access [Office development in Visual Studio]
- data [Office development in Visual Studio], accessing on server
- documents [Office development in Visual Studio], server-side data access
- workbooks [Office development in Visual Studio], inserting data
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8d9dcd22ca124ee5ea4002277f91071727a3e9e1
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985432"
---
# <a name="walkthrough-insert-data-into-a-workbook-on-a-server"></a>演练：将数据插入到服务器上的工作簿
  本演练演示如何将数据插入到在 Microsoft Office Excel 工作簿中缓存的数据集，而无需使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 类启动 Excel。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 本演练阐释了以下任务：

- 定义包含 AdventureWorksLT 数据库中的数据的数据集。

- 在 Excel 工作簿项目和控制台应用程序项目中创建数据集的实例。

- 创建绑定到工作簿中的数据集的 <xref:Microsoft.Office.Tools.Excel.ListObject>。

- 将工作簿中的数据集添加到数据缓存。

- 通过在控制台应用程序中运行代码将数据插入缓存的数据集中，而不启动 Excel。

  虽然本演练假定你在开发计算机上运行代码，但本演练演示的代码可以在未安装 Excel 的服务器上使用。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>Prerequisites
 你需要以下组件来完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- 访问 Microsoft SQL Server 或附加了 AdventureWorksLT 示例数据库的 Microsoft SQL Server Express 的正在运行的实例。 可以从[CodePlex 网站](https://archive.codeplex.com/?p=SqlServerSamples)下载 AdventureWorksLT 数据库。 有关附加数据库的详细信息，请参阅下列主题：

  - 若要使用 SQL Server Management Studio 或 SQL Server Management Studio Express 附加数据库，请参阅[如何：附加数据库（SQL Server Management Studio）](/sql/relational-databases/databases/attach-a-database)。

  - 若要使用命令行来附加数据库，请参阅[如何：将数据库文件附加到 SQL Server Express](/previous-versions/sql/)。

## <a name="create-a-class-library-project-that-defines-a-dataset"></a>创建用于定义数据集的类库项目
 若要在 Excel 工作簿项目和控制台应用程序中使用相同的数据集，则必须在这两个项目都引用的单独程序集中定义该数据集。 对于本演练，请在类库项目中定义数据集。

### <a name="to-create-the-class-library-project"></a>创建类库项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在 **“文件”** 菜单上，指向 **“新建”** ，然后单击 **“项目”** 。

3. 在 "模板" 窗格中，展开 "**视觉对象C#**  " 或 " **Visual Basic**"，然后单击 " **Windows**"。

4. 在项目模板列表中 **，选择 "类库"** 。

5. 在 "**名称**" 框中，键入**AdventureWorksDataSet**。

6. 单击 "**浏览**"，导航到 *%UserProfile%\My 文档*（适用于 windows XP 及更低版本）或 *%UserProfile%\Documents* （适用于 windows Vista）文件夹，然后单击 "**选择文件夹**"。

7. 在 "**新建项目**" 对话框中，确保未选中 "**创建解决方案的目录**" 复选框。

8. 单击“确定”。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将**AdventureWorksDataSet**项目添加到**解决方案资源管理器**，并打开**Class1.cs**或**Class1**代码文件。

9. 在**解决方案资源管理器**中，右键单击**Class1.cs**或**Class1**，然后单击 "**删除**"。 对于本演练，不需要此文件。

## <a name="define-a-dataset-in-the-class-library-project"></a>在类库项目中定义数据集
 定义一个类型化数据集，其中包含 AdventureWorksLT 数据库中 SQL Server 2005 的数据。 稍后在本演练中，你将从 Excel 工作簿项目和控制台应用程序项目引用此数据集。

 数据集是一个*类型化数据集*，它表示 AdventureWorksLT 数据库的 Product 表中的数据。 有关类型化数据集的详细信息，请参阅[Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)。

### <a name="to-define-a-typed-dataset-in-the-class-library-project"></a>定义类库项目中的类型化数据集

1. 在**解决方案资源管理器**中，单击**AdventureWorksDataSet**项目。

2. 如果 "**数据源**" 窗口不可见，请在菜单栏上选择 "**视图**"，然后选择 "查看 > **其他 Windows** > **数据源**"。

3. 选择 **“添加新数据源”** 以启动 **“数据源配置向导”** 。

4. 单击“数据库”，然后单击“下一步”。

5. 如果有与 AdventureWorksLT 数据库的连接，请选择此连接，然后单击 "**下一步**"。

    否则，单击“新建连接”，然后使用“添加连接” 对话框创建新连接。 有关详细信息，请参阅[如何：连接到数据库中的数据](../vsto/walkthrough-inserting-data-into-a-workbook-on-a-server.md)。

6. 在“将连接字符串保存到应用程序配置文件中” 页中，单击“下一步”。

7. 在 "**选择数据库对象**" 页上，展开 "**表**" 并选择 " **Product （SalesLT）** "。

8. 单击 **“完成”** 。

    *Adventureworksltdataset.xsd*文件将添加到**AdventureWorksDataSet**项目中。 此文件定义以下各项：

   - 一个名为 `AdventureWorksLTDataSet`的类型化数据集。 此数据集表示 AdventureWorksLT 数据库中的 Product 表的内容。

   - 名为 `ProductTableAdapter`的 TableAdapter。 此 TableAdapter 可用于读取和写入 `AdventureWorksLTDataSet`中的数据。 有关详细信息，请参阅[TableAdapter 概述](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview)。

     在本演练后面的部分中，你将使用这两个对象。

9. 在**解决方案资源管理器**中，右键单击**AdventureWorksDataSet** ，然后单击 "**生成**"。

     验证此项目是否已生成且未发生错误。

## <a name="create-an-excel-workbook-project"></a>创建 Excel 工作簿项目
 为数据接口创建一个 Excel 工作簿项目。 稍后在本演练中，你将创建一个显示数据的 <xref:Microsoft.Office.Tools.Excel.ListObject>，并将数据集的一个实例添加到工作簿中的数据缓存。

### <a name="to-create-the-excel-workbook-project"></a>创建 Excel 工作簿项目

1. 在**解决方案资源管理器**中，右键单击**AdventureWorksDataSet**解决方案，指向 "**添加**"，然后单击 "**新建项目**"。

2. 在模板窗格中，展开 **“Visual C#”** 或 **“Visual Basic”** ，然后展开 **“Office/SharePoint”** 。

3. 在展开的 **“Office/SharePoint”** 节点下方，选择 **“Office 外接程序”** 节点。

4. 在项目模板列表中，选择 **“Excel 2010 工作簿”** 或 **“Excel 2013 工作簿”** 项目。

5. 在 "**名称**" 框中，键入**AdventureWorksReport**。 请勿修改位置。

6. 单击“确定”。

     将打开“Visual Studio Tools for Office 项目向导” 。

7. 确保已选中 "**创建新文档**"，然后单击 **"确定"** 。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 在设计器中打开**AdventureWorksReport**工作簿，并将**AdventureWorksReport**项目添加到**解决方案资源管理器**中。

## <a name="add-the-dataset-to-data-sources-in-the-excel-workbook-project"></a>将数据集添加到 Excel 工作簿项目中的数据源
 在 Excel 工作簿中显示数据集之前，必须先将该数据集添加到 Excel 工作簿项目中的数据源。

### <a name="to-add-the-dataset-to-the-data-sources-in-the-excel-workbook-project"></a>将数据集添加到 Excel 工作簿项目中的数据源

1. 在**解决方案资源管理器**中，双击**AdventureWorksReport**项目下的 " **Sheet1.cs** " 或 " **Sheet1"。**

     工作簿将在设计器中打开。

2. 在 **“数据”** 菜单上，单击 **“添加新数据源”** 。

     “数据源配置”向导随即打开。

3. 单击 "**对象**"，然后单击 "**下一步**"。

4. 在 "**选择要绑定到的对象**" 页上，单击 "**添加引用**"。

5. 在 "**项目**" 选项卡上，单击 " **AdventureWorksDataSet** "，然后单击 **"确定"** 。

6. 在**AdventureWorksDataSet**程序集的**AdventureWorksDataSet**命名空间下，单击 " **adventureworksltdataset.xsd** "，然后单击 "**完成**"。

     此时将打开 "**数据源**" 窗口，并将**adventureworksltdataset.xsd**添加到数据源列表。

## <a name="create-a-listobject-that-is-bound-to-an-instance-of-the-dataset"></a>创建绑定到数据集实例的 ListObject
 若要在工作簿中显示数据集，请创建一个绑定到数据集实例的 <xref:Microsoft.Office.Tools.Excel.ListObject>。 有关将控件绑定到数据的详细信息，请参阅将[数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)。

### <a name="to-create-a-listobject-that-is-bound-to-an-instance-of-the-dataset"></a>创建绑定到数据集实例的 ListObject

1. 在 "**数据源**" 窗口中，展开 " **AdventureWorksDataSet**" 下的**adventureworksltdataset.xsd**节点。

2. 选择 "**产品**" 节点，单击显示的下拉箭头，然后在下拉列表中选择 " **ListObject** "。

     如果下拉箭头未出现，请确认已在设计器中打开该工作簿。

3. 将**Product**表拖到单元格 A1。

     在工作表上创建一个名为 `productListObject` <xref:Microsoft.Office.Tools.Excel.ListObject> 控件，从 A1 单元格开始。 同时，向项目添加了一个名为 `adventureWorksLTDataSet` 的数据集对象和一个名为 <xref:System.Windows.Forms.BindingSource> 的 `productBindingSource` 。 已将 <xref:Microsoft.Office.Tools.Excel.ListObject> 绑定到 <xref:System.Windows.Forms.BindingSource>，而后者又绑定到该数据集对象。

## <a name="add-the-dataset-to-the-data-cache"></a>将数据集添加到数据缓存
 若要使 Excel 工作簿项目外的代码可以访问工作簿中的数据集，则必须将数据集添加到数据缓存中。 有关数据缓存的详细信息，请参阅[文档级自定义项中的缓存数据](../vsto/cached-data-in-document-level-customizations.md)和[缓存数据](../vsto/caching-data.md)。

### <a name="to-add-the-dataset-to-the-data-cache"></a>将数据集添加到数据缓存

1. 在设计器中，单击 " **adventureworksltdataset.xsd**"。

2. 在 "**属性**" 窗口中，将 "**修饰符**" 属性设置为 "**公共**"。

3. 将**CacheInDocument**属性设置为**True**。

## <a name="checkpoint"></a>检查点
 生成并运行 Excel 工作簿项目，以确保它在编译和运行时不会出错。

### <a name="to-build-and-run-the-project"></a>生成并运行此项目

1. 在**解决方案资源管理器**中，右键单击**AdventureWorksReport**项目，选择 "**调试**"，然后单击 "**启动新实例**"。

     项目已生成，工作簿在 Excel 中打开。 **Sheet1**中的 <xref:Microsoft.Office.Tools.Excel.ListObject> 为空，因为数据缓存中的 `adventureWorksLTDataSet` 对象尚无数据。 在下一部分中，你将使用控制台应用程序来用数据填充 `adventureWorksLTDataSet` 的对象。

2. 关闭 Excel。 不保存更改。

## <a name="create-a-console-application-project"></a>创建控制台应用程序项目
 创建一个控制台应用程序项目，用于将数据插入到工作簿中的缓存数据集。

### <a name="to-create-the-console-application-project"></a>创建控制台应用程序项目

1. 在**解决方案资源管理器**中，右键单击**AdventureWorksDataSet**解决方案，指向 "**添加**"，然后单击 "**新建项目**"。

2. 在 "**项目类型**" 窗格中，展开 "**视觉对象C#**  " 或 " **Visual Basic**"，然后单击 " **Windows**"。

3. 在 "**模板**" 窗格中选择 "**控制台应用程序**"。

4. 在 "**名称**" 框中，键入**DataWriter**。 请勿修改位置。

5. 单击“确定”。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将**DataWriter**项目添加到**解决方案资源管理器**，并打开**Program.cs**或**Module1**代码文件。

## <a name="add-data-to-the-cached-dataset-by-using-the-console-application"></a>使用控制台应用程序将数据添加到缓存的数据集
 使用控制台应用程序中的 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 类来用数据填充工作簿中缓存的数据集。

### <a name="to-add-data-to-the-cached-dataset"></a>将数据添加到缓存的数据集

1. 在**解决方案资源管理器**中，右键单击**DataWriter**项目，然后单击 "**添加引用**"。

2. 在 " **.net** " 选项卡上，选择 " **VisualStudio**"。

3. 单击“确定”。

4. 在**解决方案资源管理器**中，右键单击**DataWriter**项目，然后单击 "**添加引用**"。

5. 在 "**项目**" 选项卡上，选择 " **AdventureWorksDataSet**"，然后单击 **"确定"** 。

6. 在代码编辑器中打开*Program.cs*或*Module1*文件。

7. **使用**（ C#）将以下语句添加到代码文件的顶部（对于），或将其**导入**（对于 Visual Basic）语句。

    [!code-csharp[Trin_CachedDataWalkthroughs#1](../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs#1)]
    [!code-vb[Trin_CachedDataWalkthroughs#1](../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb#1)]

8. 将以下代码添加到 `Main` 方法中。 此代码声明了下列对象：

   - **AdventureWorksDataSet**项目中定义的 `AdventureWorksLTDataSet` 和 `ProductTableAdapter` 类型的实例。

   - **AdventureWorksReport**项目的 build 文件夹中 AdventureWorksReport 工作簿的路径。

   - 用于访问工作簿中的数据缓存的 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 对象。

     > [!NOTE]
     > 以下代码假定你使用的是扩展名为 *.xlsx*的工作簿。 如果项目中的工作簿具有不同的文件扩展名，请根据需要修改路径。

     [!code-csharp[Trin_CachedDataWalkthroughs#3](../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs#3)]
     [!code-vb[Trin_CachedDataWalkthroughs#3](../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb#3)]

9. 将以下代码添加到 `Main` 方法，并在上一步中添加的代码之后。 这段代码执行下列任务：

   - 它使用表适配器填充类型化数据集对象。

   - 它使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 类的 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> 属性访问工作簿中缓存的数据集。

   - 它使用 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A> 方法，用本地类型化数据集中的数据填充缓存的数据集。

     [!code-csharp[Trin_CachedDataWalkthroughs#4](../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs#4)]
     [!code-vb[Trin_CachedDataWalkthroughs#4](../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb#4)]

10. 在**解决方案资源管理器**中，右键单击**DataWriter**项目，指向 "**调试**"，然后单击 "**启动新实例**"。

     项目将生成，并且当应用程序将数据保存到工作簿中缓存的数据集时，控制台应用程序将显示若干状态消息。 按**enter**关闭该应用程序。

## <a name="test-the-workbook"></a>测试工作簿
 打开工作簿时，<xref:Microsoft.Office.Tools.Excel.ListObject> 现在会显示通过使用控制台应用程序添加到缓存的数据集的数据。

### <a name="to-test-the-workbook"></a>测试工作簿

1. 如果 Visual Studio 设计器中的 AdventureWorksReport 工作簿仍处于打开状态，请将其关闭。

2. 在文件资源管理器中，打开 AdventureWorksReport 工作簿，该工作簿位于**AdventureWorksReport**项目的 build 文件夹中。 默认情况下，build 文件夹位于以下位置之一：

    - *%UserProfile%\My Documents\AdventureWorksReport\bin\Debug* （适用于 Windows XP 及更早版本）

    - *%UserProfile%\Documents\AdventureWorksReport\bin\Debug* （适用于 Windows Vista）

3. 在打开工作簿后，验证 <xref:Microsoft.Office.Tools.Excel.ListObject> 是否已填充数据。

## <a name="next-steps"></a>后续步骤

有关使用缓存数据的详细信息，请参阅以下主题：

- 更改缓存数据集中的数据而不启动 Excel。 有关详细信息，请参阅[演练：更改服务器上工作簿中的缓存数据](../vsto/walkthrough-changing-cached-data-in-a-workbook-on-a-server.md)。

## <a name="see-also"></a>请参阅

- [演练：更改服务器上的工作簿中的缓存数据](../vsto/walkthrough-changing-cached-data-in-a-workbook-on-a-server.md)
