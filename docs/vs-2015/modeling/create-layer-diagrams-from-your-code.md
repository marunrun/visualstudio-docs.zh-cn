---
title: Create layer diagrams from your code | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- architecture, layer diagrams
- layer diagrams
- diagrams - modeling, layer
- constraints, architectural
ms.assetid: 58c3ea71-2dbc-4963-bf82-40f1924cf973
caps.latest.revision: 64
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3e6cd77e785adb59fc8b2cf3b28724ed0efe1ae3
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300272"
---
# <a name="create-layer-diagrams-from-your-code"></a>从你的代码创建层关系图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

To visualize your software system's high-level, logical architecture, create a *layer diagram* in Visual Studio. 若要确保你的代码与此设计保持一致，请使用层关系图验证代码。 你可以为 Visual C# .NET 和 Visual Basic .NET 项目创建层关系图。 To see which versions of Visual Studio support this feature, see [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)

 ![Create a layer diagram](../modeling/media/layerdiagramvisualizecode.png "LayerDiagramVisualizeCode")

 A layer diagram lets you organize Visual Studio solution items into logical, abstract groups called *layers*. 你可以使用层来描述这些项目执行的主要任务或系统的主要组件。 每个层可包含描述更详细任务的其他层。 You can also specify the intended or existing *dependencies* between layers. 这些依赖项（表示为箭头）显示哪些层可以使用或当前正在使用由其他层表示的功能。 若要维护代码的体系结构控制，请在关系图上显示预期的依赖项，然后对照关系图验证代码。

## <a name="CreateDiagram"></a> Create a layer diagram
 在创建层关系图之前，请确保你的解决方案具有一个建模项目。 See [Create UML modeling projects and diagrams](../modeling/create-uml-modeling-projects-and-diagrams.md).

> [!IMPORTANT]
> 不要将现有层关系图从一个建模项目添加、拖动或复制到另一个建模项目或解决方案中的其他位置。 这将保留原始关系图中的引用，即使你更改此关系图。 这也将阻止层验证正常操作，并可能导致出现其他问题，例如，尝试打开该关系图时元素缺失或出现其他错误。
>
> 相反，请向建模项目中添加一个新的层关系图。 将源关系图中的元素复制到新关系图中。 保存建模项目和新的层关系图。

#### <a name="to-add-a-new-layer-diagram-to-a-modeling-project"></a>向建模项目中添加新层关系图

1. On the **Architecture** menu, choose **New UML or Layer Diagram**.

2. Under **Templates**, choose **Layer Diagram**.

3. 命名该关系图。

4. In **Add to Modeling Project**, browse to and select an existing modeling project in your solution.

     或

     Choose **Create a new modeling project** to add a new modeling project to the solution.

    > [!NOTE]
    > 层关系图必须存在于建模项目内。 但是，你可以将其链接到解决方案中任何位置的项。

5. 请确保保存建模项目和层关系图。

## <a name="CreateLayers"></a> Create layers from artifacts
 你可以从 Visual Studio 解决方案项（如项目、代码文件、命名空间、类和方法）中创建层。 这将自动在这些层和项（包括在层验证过程中）之间创建链接。

 你也可以将层链接到不支持验证的项（如 Word 文档或 PowerPoint 演示文稿）以便能够将层与规范或计划关联。 你还可以将层链接到项目中跨多个应用程序共享的文件，但验证过程将不包括带泛型名称（如“层 1”或“层 2”）的显示的层。

 To see if a linked item supports validation, open **Layer Explorer** and examine the **Supports Validation** property of the item. See [Managing links to artifacts](#Managing).

|**若要**|**Follow these steps**|
|------------|----------------------------|
|为单个项目创建一个层|<ol><li>将项从以下来源拖到层关系图上：<br /><br /> <ul><li>**解决方案资源管理器**<br /><br />         例如，您可以拖动文件或项目。</li><li>代码图<br /><br />         See [Map dependencies across your solutions](../modeling/map-dependencies-across-your-solutions.md) and [Use code maps to debug your applications](../modeling/use-code-maps-to-debug-your-applications.md).</li><li>**Class View** or **Object Browser**</li></ul><br />     层显示在关系图上，并链接到项目。</li><li>重命名层以反映关联代码或项目的作用。</li></ol> **Important:**  Dragging binary files to the layer diagram does not automatically add their references to modeling project. 你必须将要验证的二进制文件手动添加到建模项目中。 **To add binary files to the modeling project** <ol><li>In **Solution Explorer**, open the shortcut menu for the modeling project, and then choose **Add Existing Item**.</li><li>In the **Add Existing Item** dialog box, browse to the binary files, select them, and then choose **OK**.     二进制文件将显示在建模项目中。</li><li>In **Solution Explorer**, choose a binary file that you added, and then press **F4** to open the **Properties** window.</li><li>On each binary file, set the **Build Action** property to **Validate**.</li></ol>|
|为所有选择的项目创建单个层|同时将所有项目拖到层关系图上。<br /><br /> 一个层将出现在关系图上，并链接到所有这些项目。|
|为每个所选的项目创建一个层|Press and hold the **SHIFT** key while you drag all of the artifacts to the layer diagram at the same time. **Note:**  If you use the **SHIFT** key to select a range of items, release the key after you select the artifacts. 将这些项目拖到关系图上时再次按住该键。 <br /><br /> 每个项目的层将出现在关系图上，并链接到该项目。|
|向层中添加项目|将项目拖到层上。|
|创建新的未链接的层|In the **Toolbox**, expand the **Layer Diagram** section, and then drag a **Layer** to the layer diagram.<br /><br /> 若要添加多个层，请双击该工具。 When you are finished, choose the **Pointer** tool or press the **ESC** key.<br /><br /> - 或 -<br /><br /> Open the shortcut menu for the layer diagram, choose **Add**, and then choose **Layer**.|
|创建嵌套的层|将现有层拖到另一个层上。<br /><br /> - 或 -<br /><br /> Open the shortcut menu for a layer, choose **Add**, and then choose **Layer**.|
|创建包含两个或更多现有层的新层|Select the layers, open the shortcut menu for your selection, and then choose **Group**.|
|更改层的颜色|Set its **Color** property to the color that you want.|
|指定与层关联的项目必须不属于指定的命名空间|Type the namespaces in the layer's **Forbidden Namespaces** property. Use a semicolon ( **;** ) to separate the namespaces.|
|指定与层关联的项目不能依赖于指定的命名空间|Type the namespaces in the layer's **Forbidden Namespace Dependencies** property. Use a semicolon ( **;** ) to separate the namespaces.|
|指定与层关联的项目必须属于某个指定的命名空间|Type the namespace in the layer's **Required Namespaces** property. Use a semicolon ( **;** ) to separate the namespaces.|

 层上的数字指示链接到该层的项目数。 但在读取此数字时，请记住以下事项：

- 如果某个层链接到一个包含其他项目的项目，但该层未直接链接到其他项目，则该数字仅包括链接的项目。 但是，在层验证过程中其他项目包括在分析范围内。

     例如，如果一个层链接到单个命名空间，则链接的项目数是 1，即使该命名空间包含类也是如此。 如果该层还链接到命名空间中的每个类，则该数字将包括链接的类。

- 如果一个层包含链接到项目的其他层，则容器层也链接到这些项目，即使容器层上的数字不包括这些项目。

## <a name="Managing"></a> Manage links between layers and artifacts

1. On the layer diagram, open the shortcut menu for the layer, and then choose **View Links**.

     **Layer Explorer** shows the artifact links for the selected layer.

2. 使用以下任务管理这些链接：

|**若要**|**In Layer Explorer**|
|------------|---------------------------|
|删除层与项目之间的链接|Open the shortcut menu for the artifact link, and then choose **Delete**.|
|将链接从一个层移到另一个层|将项目链接拖到关系图上的一个现有层。<br /><br /> - 或 -<br /><br /> 1.  Open the shortcut menu for the artifact link, and then choose **Cut**.<br />2.  On the layer diagram, open the shortcut menu for the layer, and then choose **Paste**.|
|将链接从一个层复制到另一个层|1.  Open the shortcut menu for the artifact link, and then choose **Copy**.<br />2.  On the layer diagram, open the shortcut menu for the layer, and then choose **Paste**.|
|基于现有项目链接创建一个新层|将项目链接拖到关系图上的空白区域。|
|验证链接的项目是否支持对照层关系图的验证。|Look at the **Supports Validation** column for the artifact link.|

## <a name="Discovering"></a> Reverse-engineer existing dependencies
 只要与一个层关联的项目引用与另一个层关联的项目，就存在依赖关系。 例如，一个层中的某个类声明了一个拥有其他层中的某个类的变量。 你可以对关系图上链接到层的项目的现有依赖关系进行反向工程处理。

> [!NOTE]
> 无法为某些种类的项目对依赖关系进行反向工程处理。 例如，对于链接到文本文件的层，将不会对源自或指向该层的依赖关系进行反向工程处理。 To see which artifacts have dependencies that you can reverse-engineer, open the shortcut menu for one or multiple layers, and then choose **View Links**. In **Layer Explorer**, examine the **Supports Validation** column. Dependencies will not be reverse-engineered for artifacts for which this column shows **False**.

- Select one or multiple layers, open the shortcut menu for a selected layer, and then choose **Generate Dependencies**.

  通常，您会看到一些不应存在的依赖关系。 可以编辑这些依赖关系，使它们与预期的设计对齐。

## <a name="EditDependencies"></a> Edit layers and dependencies to show the intended design
 若要描述你计划对系统或计划的体系结构进行的更改，请编辑关系图：

|**若要**|**Perform these steps**|
|------------|-----------------------------|
|更改或限制依赖项的方向|Set its **Direction** property.|
|创建新的依赖项|Use the **Dependency** and **Bidirectional Dependency** tools.<br /><br /> 若要绘制多个依赖关系，请双击该工具。 When you are finished, choose the **Pointer** tool or press the **ESC** key.|
|指定与层关联的项目不能依赖于指定的命名空间|Type the namespaces in the layer's **Forbidden Namespace Dependencies** property. Use a semicolon ( **;** ) to separate the namespaces.|
|指定与层关联的项目必须不属于指定的命名空间|Type the namespaces in the layer's **Forbidden Namespaces** property. Use a semicolon ( **;** ) to separate the namespaces.|
|指定与层关联的项目必须属于某个指定的命名空间|Type the namespace in the layer's **Required Namespaces** property. Use a semicolon ( **;** ) to separate the namespaces.|

## <a name="EditLayout"></a> Change how elements appear on the diagram
 通过编辑层或依赖项的属性，你可以更改层的大小、形状、颜色和位置或依赖项的颜色。

## <a name="Codemaps"></a> Discover patterns and dependencies on a code map
 While creating layer diagrams, you might also create **code maps**. 这些关系图可以帮助你在浏览代码时发现模式和依赖项。 使用解决方案资源管理器、类视图或对象浏览器来浏览程序集、命名空间和类，这通常能很好地响应现有层。 有关代码图的详细信息，请参阅：

- [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)

- [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)

- [使用代码图分析查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)

## <a name="see-also"></a>请参阅
 [Channel 9 Video: Design and validate your architecture using layer diagrams](https://go.microsoft.com/fwlink/?LinkID=252073) [Layer Diagrams: Reference](../modeling/layer-diagrams-reference.md) [Layer Diagrams: Guidelines](../modeling/layer-diagrams-guidelines.md) [Validate code with layer diagrams](../modeling/validate-code-with-layer-diagrams.md) [Visualize code](../modeling/visualize-code.md)