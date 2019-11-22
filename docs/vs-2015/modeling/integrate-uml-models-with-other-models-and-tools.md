---
title: Integrate UML models with other models and tools | Microsoft Docs
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
ms.openlocfilehash: caecb85392170559a860a7dc334570880d6e76f1
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301471"
---
# <a name="integrate-uml-models-with-other-models-and-tools"></a>将 UML 模型与其他模型和工具集成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML 模型可与其他模型和特定于域的语言集成。

 你可以通过编写扩展代码以如下方式集成模型，以执行各种功能：

 将任何元素中的引用附加到其他项（如文件）或其他模型中的元素。
在 UML 元素中，可以通过将其身份编码为字符串来存储指向其他 UML 元素、文件或其他对象的链接。

 例如，你可以编写一个可将任何 UML 操作（即活动图中的元素）链接到另一个活动关系图的扩展。 当用户双击该操作时，将打开另一个关系图。 这使得用户能够提供该操作的更详细视图。

 可以采用两种方法将字符串和其他数据存储在任何元素中：

- **Stereotype properties.** 可以定义 UML 配置文件，并在其中定义可将属性添加到指定类型的 UML 元素的构造型。 For example, you could define a profile that adds a property named **MoreDetail** to a UML action. 通过向操作应用构造型，然后将数据存储在属性中，可以编写将链接数据存储在操作中的扩展代码。

   用户可以在“属性”窗口看到构造型及其属性。

   若要部署此扩展，请将配置文件定义和扩展代码打包到单个 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展中。

   For more information, see [Define a profile to extend UML](../modeling/define-a-profile-to-extend-uml.md).

   For a sample project in which a profile is deployed together with menu commands and gesture handlers, see [Sample: UML Profiles](https://go.microsoft.com/fwlink/?LinkID=213811).

- **References.** 你可以将一组字符串附加到任何 UML 元素。 你可以编写用于存储信息的代码，如另一个元素的文件名或 GUID。 无需提供其他定义就可完成此操作。 引用并不直接对用户可见。

   For more information, see [Attach reference strings to UML model elements](../modeling/attach-reference-strings-to-uml-model-elements.md). For a sample, see [Link UML Elements to Diagrams or other Files](https://go.microsoft.com/fwlink/?LinkId=213813).

  有两种方法可以对模型元素的引用进行编码：

- **GUID and Filename** of the target model element and the model that contains it, or a particular diagram that displays it.

   For an example, see [Link UML Elements to Diagrams or other Files](https://go.microsoft.com/fwlink/?LinkId=213813).

- **ModelBus References.** ModelBus 是用于创建和解析模型之间的引用的框架。 它包括 ModelBus 选取器，允许用户选择某一模型中的元素。 它还帮助用户解决由于目标模型中的更改而丢失的引用。

   For more information, see [Integrating Models by using Visual Studio Modelbus](../modeling/integrating-models-by-using-visual-studio-modelbus.md).

  将更改从一个模型传播到另一个模型。
  例如，你可以使元素的名称与所链接关系图的名称保持同步，以便在用户更改其中一个名称时，另一个名称也随之更改。 有两种机制可用于实现此操作：

1. **VMSDK Rules** can be used to propagate changes inside the same model.

    For an example, see [Link UML Elements to Diagrams or other Files](https://go.microsoft.com/fwlink/?LinkId=213813).

2. **VMSDK Events** can be used to propagate changes outside the model – for example, to change the filename of a linked document, or to change an element in another model.

   For information about both these mechanisms, see [How to: Respond to Changes in a UML Model](../misc/how-to-respond-to-changes-in-a-uml-model.md).

   Drag elements to copy them from one model to another You can let the user create elements by dragging items onto a UML diagram. 创建的元素不必是原始元素的副本。 例如，你可以让用户将一个活动关系图从解决方案资源管理器拖到另一个活动关系图上，以创建新的操作。

   For more information see [Define a gesture handler on a modeling diagram](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md) and [How to: Add a Drag-and-Drop Handler](../modeling/how-to-add-a-drag-and-drop-handler.md).

## <a name="samples"></a>示例
 Please see the code sample [Link UML Elements to Diagrams or other Files](https://go.microsoft.com/fwlink/?LinkId=213813). 此示例允许用户将文件拖到任何 UML 元素上，并在之后通过双击该元素来打开该文件。 例如，可以将活动关系图链接到用例元素。 图标显示哪些元素具有链接。

 此代码示例演示以下技术：

- [将引用字符串附加到 UML 模型元素](../modeling/attach-reference-strings-to-uml-model-elements.md)

   示例代码将文件路径和元素 GUID 存储在与元素关联的引用字符串中。

- 如何将修饰器添加到 UML 元素。 For general information about decorators, see [Customizing Text and Image Fields](../modeling/customizing-text-and-image-fields.md).

   该示例将图像修饰器添加到 UML 形状。

- [如何：响应 UML 模型中的更改](../misc/how-to-respond-to-changes-in-a-uml-model.md)

   此示例演示如何定义对关系图中显示的新形状作出响应的规则。

- [在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)

- [在建模图上定义笔势处理程序](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)

   此示例演示如何处理从 Windows 资源管理器（或文件资源管理器）、解决方案资源管理器及其他 UML 元素拖动的项。

  For an example in which a UML model is be read by a DSL, see [How to: Add a Drag-and-Drop Handler](../modeling/how-to-add-a-drag-and-drop-handler.md).

## <a name="see-also"></a>请参阅
 [Define a menu command on a modeling diagram](../modeling/define-a-menu-command-on-a-modeling-diagram.md) [Define a gesture handler on a modeling diagram](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md) [How to: Add a Drag-and-Drop Handler](../modeling/how-to-add-a-drag-and-drop-handler.md) [How to: Respond to Changes in a UML Model](../misc/how-to-respond-to-changes-in-a-uml-model.md) [Sample: UML Profiles](https://go.microsoft.com/fwlink/?LinkID=213811) [Link UML Elements to Diagrams or other Files](https://go.microsoft.com/fwlink/?LinkId=213813)
