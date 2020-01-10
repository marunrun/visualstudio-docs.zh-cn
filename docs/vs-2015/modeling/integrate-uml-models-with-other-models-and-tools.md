---
title: 将 UML 模型与其他模型和工具集成 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML - extending, references to models
ms.assetid: 9e75e7d1-93cf-4196-baa3-bd10b9af16d3
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 87d7742c988e0193c8175621a08478b6225c8670
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850647"
---
# <a name="integrate-uml-models-with-other-models-and-tools"></a>将 UML 模型与其他模型和工具集成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML 模型可与其他模型和特定于域的语言集成。

 你可以通过编写扩展代码以如下方式集成模型，以执行各种功能：

 将任何元素中的引用附加到其他项（如文件）或其他模型中的元素。
在 UML 元素中，可以通过将其身份编码为字符串来存储指向其他 UML 元素、文件或其他对象的链接。

 例如，你可以编写一个可将任何 UML 操作（即活动图中的元素）链接到另一个活动关系图的扩展。 当用户双击该操作时，将打开另一个关系图。 这使得用户能够提供该操作的更详细视图。

 可以采用两种方法将字符串和其他数据存储在任何元素中：

- **构造型属性。** 可以定义 UML 配置文件，并在其中定义可将属性添加到指定类型的 UML 元素的构造型。 例如，可以定义一个配置文件，用于将名为**MoreDetail**的属性添加到 UML 操作中。 通过向操作应用构造型，然后将数据存储在属性中，可以编写将链接数据存储在操作中的扩展代码。

   用户可以在“属性”窗口看到构造型及其属性。

   若要部署此扩展，请将配置文件定义和扩展代码打包到单个 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展中。

   有关详细信息，请参阅[定义用于扩展 UML 的配置文件](../modeling/define-a-profile-to-extend-uml.md)。

   有关将配置文件与菜单命令和笔势处理程序一起部署的示例项目，请参阅[示例： UML 配置文件](https://docs.microsoft.com/samples/browse/?redirectedfrom=MSDN-samples)。

- **参考.** 你可以将一组字符串附加到任何 UML 元素。 你可以编写用于存储信息的代码，如另一个元素的文件名或 GUID。 无需提供其他定义就可完成此操作。 引用并不直接对用户可见。

   有关详细信息，请参阅[将引用字符串附加到 UML 模型元素](../modeling/attach-reference-strings-to-uml-model-elements.md)。 有关示例，请参阅[将 UML 元素链接到关系图或其他文件](https://docs.microsoft.com/samples/browse/?redirectedfrom=MSDN-samples)。

  有两种方法可以对模型元素的引用进行编码：

- 目标模型元素的**GUID 和文件名**以及包含它的模型或显示该元素的特定关系图。

   有关示例，请参阅[将 UML 元素链接到关系图或其他文件](https://docs.microsoft.com/samples/browse/?redirectedfrom=MSDN-samples)。

- **ModelBus 引用。** ModelBus 是用于创建和解析模型之间的引用的框架。 它包括 ModelBus 选取器，允许用户选择某一模型中的元素。 它还帮助用户解决由于目标模型中的更改而丢失的引用。

   有关详细信息，请参阅[使用 Visual Studio 集成模型 Modelbus](../modeling/integrating-models-by-using-visual-studio-modelbus.md)。

  将更改从一个模型传播到另一个模型。
  例如，你可以使元素的名称与所链接关系图的名称保持同步，以便在用户更改其中一个名称时，另一个名称也随之更改。 有两种机制可用于实现此操作：

1. **VMSDK 规则**可用于在同一模型内传播更改。

    有关示例，请参阅[将 UML 元素链接到关系图或其他文件](https://docs.microsoft.com/samples/browse/?redirectedfrom=MSDN-samples)。

2. **VMSDK 事件**可用于在模型外传播更改（例如，更改链接文档的文件名）或更改另一个模型中的元素。

   有关这两种机制的详细信息，请参阅[如何：响应 UML 模型中的更改](../misc/how-to-respond-to-changes-in-a-uml-model.md)。

   拖动元素以将其从一个模型复制到另一个模型，可让用户通过将项拖到 UML 关系图上来创建元素。 创建的元素不必是原始元素的副本。 例如，你可以让用户将一个活动关系图从解决方案资源管理器拖到另一个活动关系图上，以创建新的操作。

   有关详细信息，请参阅[在建模图上定义笔势处理程序](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)和[如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)。

## <a name="samples"></a>示例
 请参阅代码示例：将[UML 元素链接到关系图或其他文件](https://docs.microsoft.com/samples/browse/?redirectedfrom=MSDN-samples)。 此示例允许用户将文件拖到任何 UML 元素上，并在之后通过双击该元素来打开该文件。 例如，可以将活动关系图链接到用例元素。 图标显示哪些元素具有链接。

 此代码示例演示以下技术：

- [将引用字符串附加到 UML 模型元素](../modeling/attach-reference-strings-to-uml-model-elements.md)

   示例代码将文件路径和元素 GUID 存储在与元素关联的引用字符串中。

- 如何将修饰器添加到 UML 元素。 有关修饰器的常规信息，请参阅[自定义文本和图像字段](../modeling/customizing-text-and-image-fields.md)。

   该示例将图像修饰器添加到 UML 形状。

- [如何：响应 UML 模型中的更改](../misc/how-to-respond-to-changes-in-a-uml-model.md)

   此示例演示如何定义对关系图中显示的新形状作出响应的规则。

- [在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)

- [在建模图上定义笔势处理程序](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)

   此示例演示如何处理从 Windows 资源管理器（或文件资源管理器）、解决方案资源管理器及其他 UML 元素拖动的项。

  有关 DSL 读取 UML 模型的示例，请参阅[如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)。

## <a name="see-also"></a>请参阅
 [在建模图上定义菜单命令在](../modeling/define-a-menu-command-on-a-modeling-diagram.md)[建模图上定义笔势处理程序](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)[如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)[如何：响应 UML 模型中的更改](../misc/how-to-respond-to-changes-in-a-uml-model.md)[示例： Uml 配置文件](https://docs.microsoft.com/samples/browse/?redirectedfrom=MSDN-samples)将[uml 元素链接到关系图或其他文件](https://docs.microsoft.com/samples/browse/?redirectedfrom=MSDN-samples)
