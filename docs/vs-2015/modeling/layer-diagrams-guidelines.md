---
title: 'Layer Diagrams: Guidelines | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- architecture, layer diagrams
- layer diagrams
- diagrams - modeling, layer
- constraints, architectural
ms.assetid: 2903bec7-a93b-46a6-aac6-994ac4f3f1a7
caps.latest.revision: 57
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 51cb71d4bc2f66377b677d5be292c4eafa1dbd18
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299465"
---
# <a name="layer-diagrams-guidelines"></a>层关系图：指南
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Describe your app's architecture at a high level by creating *layer diagrams* in Visual Studio. 若要确保你的代码与此设计保持一致，请使用层关系图验证代码。 还可以在生成过程中包括层验证。 See [Channel 9 Video: Design and validate your architecture using layer diagrams](https://go.microsoft.com/fwlink/?LinkID=252073).

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="what-is-a-layer-diagram"></a>什么是层关系图?
 类似于传统的体系结构示意图，层关系图标识设计的主要组件或功能单元及其相互依赖关系。 Each node on the diagram, called a *layer*, represents a logical group of namespaces, projects, or other artifacts. 您可以绘制出您的设计中存在的依赖关系。 与传统的体系结构关系图不同的是，您可以验证源代码中的实际依赖关系符合您指定的预期依赖关系。 通过在[!INCLUDE[esprtfs](../includes/esprtfs-md.md)]上验证常规生成的一部分，您可以确保程序代码继续符合系统的体系结构将来的更改。 See [Layer Diagrams: Reference](../modeling/layer-diagrams-reference.md).

## <a name="Update"></a> How to design or update your app with layer diagrams
 以下步骤概述了如何使用开发过程中的层关系图。 本主题中的后面几节描述了有关每个步骤的更多详细信息。 如果你正在开发新的设计，请忽略引用现有代码的步骤。

> [!NOTE]
> 这些步骤按大致顺序显示。 您可能需要重叠任务、重新排序它们以符合您自己的具体情况，并在项目中的每个迭代开始时重新访问它们。

1. [Create a layer diagram](#Create) for the whole application, or for a layer within it.

2. [Define layers to represent primary functional areas or components](#CreateLayers) of your application. 按其功能命名这些层，例如“演示文稿”或“服务”。 If you have a [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] solution, you can associate each layer with a collection of *artifacts*, such as projects, namespaces, files, and so on.

3. [Discover the existing dependencies](#Generate) between layers.

4. [Edit the layers and dependencies](#EditArchitecture) to show the updated design that you want the code to reflect.

5. [Design new areas of your application](#NewAreas) by creating layers to represent the principal architectural blocks or components and defining dependencies to show how each layer uses the others.

6. [Edit the layout and appearance of the diagram](#EditLayout) to help you discuss it with colleagues.

7. [Validate the code against the layer diagram](#Validate) to highlight the conflicts between the code and the architecture you require.

8. [Update the code to conform to your new architecture](#UpdateCode). 以迭代方式开发和重构代码，直到此验证不再显示有冲突。

9. [Include layer validation in the build process](#BuildValidation) to ensure that the code continues to adhere to your design.

## <a name="Create"></a> Create a layer diagram
 必须在建模项目内创建层关系图。 可以将新的层关系图添加到现有建模项目、为层关系图创建新的建模项目或在同一建模项目中复制现有层关系图。

> [!IMPORTANT]
> 不要将现有层关系图从一个建模项目添加、拖动或复制到另一个建模项目或解决方案中的其他位置。 以这种方式中复制的层关系图将具有与原始关系图相同的引用，即使您修改了关系图。 这将阻止层验证正常操作，并可能导致出现其他问题，例如，尝试打开该关系图时元素缺失或出现其他错误。

 See [Create layer diagrams from your code](../modeling/create-layer-diagrams-from-your-code.md).

## <a name="CreateLayers"></a> Define layers to represent functional areas or components
 Layers represent logical groups of *artifacts*, such as projects, code files, namespaces, classes, and methods. 可以从 Visual C# .NET 和 Visual Basic .NET 项目创建层，也可以通过链接文档（如 Word 文件或 PowerPoint 演示文稿）将规范或计划附加到层。 每一层显示为关系图上的一个矩形，并显示链接到它的项目数。 一个层可以包含描述更具体任务的嵌套的层。

 一般原则是按其功能命名层，例如“演示文稿”或“服务”。 如果这些项目依赖关系紧密，则将它们放在同一层。 如果可以分别更新或在单独的应用程序中使用这些项目，请将它们放在不同的层中。 To learn about layering patterns, visit the Patterns & Practices site at [http://go.microsoft.com/fwlink/?LinkId=145794](https://go.microsoft.com/fwlink/?LinkId=145794).

> [!TIP]
> 有某些类型的可链接到层的项目，但是不支持对层关系图进行验证。 To see whether the artifact supports validation, open **Layer Explorer** to examine the **Supports Validation** property of the artifact link. See [Discover existing dependencies between layers](#Generate).

 更新不熟悉的应用程序时，你也可以创建代码图。 这些关系图可以帮助你在浏览代码时发现模式和依赖项。 使用解决方案资源管理器来浏览命名空间和类，它们通常与现有层具有很好的对应关系。 通过将代码项目从解决方案资源管理器拖动至层关系图来对其进行分配。 然后可以使用层关系图来帮助你更新代码，并使其与你的设计保持一致。

 请参阅：

- [从代码创建层关系图](../modeling/create-layer-diagrams-from-your-code.md)

- [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)

- [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)

## <a name="Generate"></a> Discover existing dependencies between layers
 只要与一个层关联的项目引用与另一个层关联的项目，就存在依赖关系。 例如，一个层中的某个类声明了一个拥有其他层中的某个类的变量。 您可以对它们实施反向工程来发现现有依赖关系。

> [!NOTE]
> 无法为某些种类的项目对依赖关系进行反向工程处理。 例如，对于链接到文本文件的层，将不会对源自或指向该层的依赖关系进行反向工程处理。 To see which artifacts have dependencies that you can reverse-engineer, right-click one or multiple layers, and then click **View Links**. In **Layer Explorer**, examine the **Supports Validation** column. Dependencies will not be reverse-engineered for artifacts for which this column shows **False**.

#### <a name="to-reverse-engineer-existing-dependencies-between-layers"></a>为对层之间的现有依赖关系进行反向工程

- Select one layer or multiple layers, right-click a selected layer, and then click **Generate Dependencies**.

  通常，您会看到一些不应存在的依赖关系。 可以编辑这些依赖关系，使它们与预期的设计对齐。

## <a name="EditArchitecture"></a> Edit layers and dependencies to show the intended design
 若要说明您准备对系统或计划的体系结构进行的更改，请使用以下步骤来编辑层关系图。 你还可以考虑进行一些重构的更改，以提高代码的结构，然后再扩展。 See [Improving the structure of the code](#Improving).

|**若要**|**Perform these steps**|
|------------|-----------------------------|
|删除不应存在的依赖项|Click the dependency, and then press **DELETE**.|
|更改或限制依赖项的方向|Set its **Direction** property.|
|创建新的依赖项|Use the **Dependency** and **Bidirectional Dependency** tools.<br /><br /> 若要绘制多个依赖关系，请双击该工具。 When you are finished, click the **Pointer** tool or press the **ESC** key.|
|指定与层关联的项目不能依赖于指定的命名空间|Type the namespaces in the layer's **Forbidden Namespace Dependencies** property. Use a semicolon ( **;** ) to separate the namespaces.|
|指定与层关联的项目必须不属于指定的命名空间|Type the namespaces in the layer's **Forbidden Namespaces** property. Use a semicolon ( **;** ) to separate the namespaces.|
|指定与层关联的项目必须属于某个指定的命名空间|Type the namespace in the layer's **Required Namespaces** property. Use a semicolon ( **;** ) to separate the namespaces.|

### <a name="Improving"></a> Improving the structure of the code
 重构更改的改进不会影响应用程序的行为，但有助于使代码在将来更易于更改和扩展。 结构良好的代码的设计容易抽象化为层关系图。

 例如，如果你为代码中的每个命名空间创建图层，然后进行反向工程处理依赖关系，各层之间应该有单向依赖项的最小集。 如果您使用类或方法创建更详细的关系图作为您的层，则结果也将具有相同的特征。

 如果不是这样，代码将会更加难以在其生命周期中更改，并且将不太适用于使用层关系图进行验证。

## <a name="NewAreas"></a> Design new areas of your application
 当你启动开发新项目或新项目中的新区域时，你可以绘制层和依赖项，以帮助你在开始开发代码之前标识主要组件。

- **Show identifiable architectural patterns** in your layer diagrams, if possible. 例如，描述桌面应用程序的层关系图可能包括演示文稿、域逻辑和数据存储等层。 涵盖应用程序的单个功能的层关系图，可能有模型、视图和控制器等一些层。 For more information about such patterns, see [Patterns & Practices: Application Architecture](https://go.microsoft.com/fwlink/?LinkId=145794).

     如果您要频繁创建相似的模式，请创建一个自定义工具。 See [Define a custom modeling toolbox item](../modeling/define-a-custom-modeling-toolbox-item.md).

- **Create a code artifact for each layer** such as a namespace, class, or component. 这样，就更容易跟踪代码，并把代码项目链接到层。 当你创建每个项目时，将其链接到相应的层。

- **You do not have to link most classes and other artifacts to layers** because they fall within larger artifacts such as namespaces that you have already linked to layers.

- **Create a new diagram for a new feature**. 通常情况下，将有一个或多个层关系图来描述整个应用程序。 如果您正在设计应用程序的新功能，请勿添加或更改现有的关系图。 相反，创建你自己的关系图来反映代码的新部分。 新关系图中的图层可能包括演示文稿、域逻辑和新功能的数据库层。

     在生成应用程序时，将同时对整体的关系图和更详细的功能关系图验证你的代码。

## <a name="EditLayout"></a> Edit the layout for presentation and discussion
 为了帮助你识别层和依赖项或与团队成员对其进行讨论，你可以按以下方式编辑关系图的外观和布局：

- 更改图层的大小、 形状和位置。

- 更改层的颜色和依赖项。

  - Select one or more layers or dependencies, right-click, and then click **Properties**. In the **Properties** window, edit the **Color** property.

## <a name="Validate"></a> Validate the code against the diagram
 编辑关系图之后，你可以对照代码随时手动验证关系图，也可以在每次运行本地生成或[!INCLUDE[esprbuild](../includes/esprbuild-md.md)]时进行自动验证。

 请参阅：

- [用层关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)

- [Include Layer Validation in the Build Process](#BuildValidation)

## <a name="UpdateCode"></a> Update the code to conform to the new architecture
 通常情况下，当你将验证更新后的层关系图的代码时，将出现第一次错误。 这些错误可能有几个原因：

- 将项目指派给了错误的层。 在这种情况下，请移动项目。

- 项目（例如类）以与你的体系结构相冲突的方式使用了其他类。 在这种情况下，请重构代码以移除依赖关系。

  若要解决这些错误，请更新代码，直至验证过程中不出现其他错误为止。 这通常是一个迭代过程。 For more information about these errors, see [Validate code with layer diagrams](../modeling/validate-code-with-layer-diagrams.md).

> [!NOTE]
> 在您开发或重构代码时，您可能有新项目要链接到层关系图。 但是，这可能不是必要的，例如，当你的层表示现有命名空间时，而且新代码只是向这些命名空间中添加更多的材料。

 在开发过程中，你可能需要在验证期间禁止显示报告的某些冲突。 例如，你可能希望禁止显示你已解决或与特定情形不相关的错误。 禁止显示错误时，最好在 [!INCLUDE[esprfound](../includes/esprfound-md.md)] 中记录工作项。 To perform this task, see [Validate code with layer diagrams](../modeling/validate-code-with-layer-diagrams.md).

## <a name="BuildValidation"></a> Include layer validation in the build process
 若要确保将来更改的代码符合层关系图，请把层验证包含到你的解决方案的标准生成过程中。 在其他团队成员生成解决方案时，代码的依赖关系和层关系图之间的差异将作为生成错误进行报告。 For more information about including layer validation in the build process, see [Validate code with layer diagrams](../modeling/validate-code-with-layer-diagrams.md).

## <a name="see-also"></a>请参阅
 [Layer Diagrams: Reference](../modeling/layer-diagrams-reference.md) [Create layer diagrams from your code](../modeling/create-layer-diagrams-from-your-code.md)
