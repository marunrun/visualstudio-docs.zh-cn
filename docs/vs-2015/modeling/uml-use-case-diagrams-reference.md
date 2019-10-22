---
title: UML 用例图：参考 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.usecasediagram.toolbox
- vs.teamarch.usecasediagram.diagram
- vs.teamarch.UMLModelExplorer.usecasediagram
helpviewer_keywords:
- diagrams - modeling, use case
- UML, use case diagrams
- diagrams - modeling, UML use case
- use case diagrams
- UML diagrams, use case
ms.assetid: aa15772b-eb67-4366-b145-b559112817df
caps.latest.revision: 35
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: cbea61c2a26b1dc81487365ef8fc3f320ac95943
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657307"
---
# <a name="uml-use-case-diagrams-reference"></a>UML 用例图：参考
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 中，*用例图*汇总了使用你的应用程序或系统的人员，以及这些用户可以对其执行的操作。 若要创建 UML 用例图，请在 "**体系结构**" 菜单上单击 "**新建 UML 或层关系图**"。

 用例图充当用户要求说明的焦点。 它描述要求、用户和主要组件之间的关系。 它不详细描述要求；这些要求可以在单独的关系图或可链接到每个用例的文档中进行描述。 有关使用例图如何帮助你了解、讨论和传达用户的需求的信息，请参阅[模型用户需求](../modeling/model-user-requirements.md)。

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

> [!NOTE]
> 本主题介绍了用例图中可用的元素。 有关如何绘制用例图的详细信息，请参阅[UML 用例图：准则](../modeling/uml-use-case-diagrams-guidelines.md)。 有关如何创建和绘制建模图的详细信息，请参阅[编辑 UML 模型和关系图](../modeling/edit-uml-models-and-diagrams.md)。

## <a name="reading-use-case-diagrams"></a>阅读用例图
 以下各节中的表介绍了用例图上可用的元素及其主要属性。 有关属性的完整列表，请参阅[UML 用例图上元素的属性](../modeling/properties-of-elements-on-uml-use-case-diagrams.md)。

### <a name="actors-use-cases-and-subsystems"></a>参与者、用例和子系统
 ![用例图中的元素](../modeling/media/uml-ucovactor.png "UML_UCOvActor")

|**整形**|**元素**|**Description 和 Main 属性**|
|---------------|-----------------|-----------------------------------------|
|1|**演员**|表示用户、组织或与你的应用程序或系统进行交互的外部系统。 参与者是一种类型。<br /><br /> -   **图像路径**-应使用的图像的文件路径，而不是默认的参与者图标。 该图标应为 Visual Studio 项目中的资源文件。|
|2|**用例**|表示由一个或多个参与者为实现特定目标而执行的操作。 用例是一种类型。<br /><br /> -   **主题**-在其中出现用例的子系统。|
|3|**关联**|指示参与者参与用例。|
|4|**子系统或组件**|正在使用的系统或应用程序或它们的一部分。 可以是任何内容，从大型网络到应用程序中的单个类。<br /><br /> 系统或组件支持的用例显示在其矩形内。 将一些用例显示在矩形外很有用，可以明确系统的作用域。<br /><br /> 基本上，用例图中的子系统具有与组件图中的组件相同的类型。<br /><br /> -   **间接实例化**-如果为 false，则您的执行系统具有一个或多个直接对应于此子系统的对象。 如果为 true，则子系统是设计中仅通过其构成部分的实例化显示在执行系统中的一个构造。|

### <a name="structuring-use-cases"></a>结构化用例
 ![包含、扩展和归纳的用例](../modeling/media/uml-ucovstructure.png "UML_UCOvStructure")

|形状|**元素**|描述|
|-----------|-----------------|-----------------|
|5|**包括**|包括用例可调用被包括用例。 包含用于显示用例如何分为更小的步骤。 被包括用例位于箭头端。<br /><br /> 请注意，此图不显示步骤顺序。 可以使用活动图、序列图或其他文档来描述这些详细信息。|
|6|**扩展**|扩展用例向被扩展用例添加目标和步骤。 扩展仅在某些情况下运行。 被扩展用例位于箭头端。<br /><br /> 请注意此图不显示应用扩展的确切情况：可以在注释或其他文档中对其进行记录|
|7|**继承**|关联专用和通用元素。 通用元素位于箭头端。<br /><br /> 专用用例继承其通用型的目标和参与者，并可添加更多特定目标和步骤来实现这些目标。<br /><br /> 专用参与者继承其通用型的用例、属性和关联，并可添加更多上述内容。|
|8|**依赖项**|指示源的设计取决于目标的设计。|
|9|**注释**|用于向关系图添加一般注释。|
|10|**伪像**|项目提供指向另一个关系图或文档的链接。 可以通过从解决方案资源管理器拖动文件来创建它。 它可以通过依赖项链接到关系图上的任何其他元素。 项目通常用于将用例链接到对其进行详细阐述的序列图、OneNote 页、Word 文档或 PowerPoint 演示文稿。 文档可以是 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 解决方案中的项，也可以是共享位置（如 SharePoint 站点）的文档。<br /><br /> -   **超链接**。 关系图或文档的 URL 或文件路径。<br /><br /> 双击项目以打开其链接到的文件或网页。|
|11（未显示）|**包**|用例、参与者和子系统可以包含在包中。 包形状不会显示在关系图上，但可以设置关系图的**LinkedPackage**属性。 随后在关系图上创建的元素将放入包中。 有关详细信息，请参阅[定义包和命名空间](../modeling/define-packages-and-namespaces.md)。|

## <a name="see-also"></a>请参阅
 [UML 用例图：准则](../modeling/uml-use-case-diagrams-guidelines.md)[编辑 uml 模型和关系图](../modeling/edit-uml-models-and-diagrams.md) [UML 序列图：引用](../modeling/uml-sequence-diagrams-reference.md)Uml[类图](../modeling/uml-class-diagrams-reference.md)：引用 uml[组件图](../modeling/uml-component-diagrams-reference.md)：引用 uml[组件图](../modeling/uml-component-diagrams-reference.md)：引用
