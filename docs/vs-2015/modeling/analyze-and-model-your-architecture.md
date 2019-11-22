---
title: Analyze and model your architecture | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Ultimate, exploring code
- Visual Studio Ultimate, visualizing code
- diagrams - modeling
- Visual Studio ALM, modeling
- application, design
- architecture
- code visualization
- application design
- applications, architecture
- code exploration
- Visual Studio ALM, exploring code
- modeling
- application architecture
- application, modeling
- applications, modeling
- architecture [Visual Studio ALM], modeling
- application modeling
- Visual Studio Ultimate, modeling
- architecture [Visual Studio Ultimate], modeling
- application, architecture
- Visual Studio ALM, visualizing code
- applications, designing
ms.assetid: c9f04cfa-72bd-419d-a952-616eed01472e
caps.latest.revision: 129
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 49c421af5aa6c91535b05f0beca88099ea7a2eaa
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297942"
---
# <a name="analyze-and-model-your-architecture"></a>对体系结构进行分析和建模
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过使用 Visual Studio 体系结构和建模工具对应用进行设计和建模确保应用满足用户要求。 通过使用 Visual Studio 来可视化代码结构、行为和关系可使你更容易理解现有程序代码。

 作为开发过程的一部分，可以跨整个应用程序生命周期创建不同详细信息级别的模型。 可通过将模型元素链接到 Team Foundation Server 工作项和开发计划来跟踪要求、任务、测试用例、Bug 和其他与模型关联的工作。 See [Scenario: Change your design using visualization and modeling](../modeling/scenario-change-your-design-using-visualization-and-modeling.md).

 若要查看支持每个功能的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)

## <a name="to"></a>功能

|||
|-|-|
|**可视化代码**：<br /><br /> -   See the code's organization and relationships by creating code maps. 可视化程序集、命名空间、类、方法等之间的依赖关系。<br />-   See the class structure and members for a specific project by creating class diagrams from code.<br />-   Find conflicts between your code and its design by creating layer diagrams to validate code.<br /><br /> **注意**：在此版本的 Visual Studio 中，术语 *代码图* 用于替换 *依赖项关系图*。 术语 *关系图* 在独立使用时，一般指定向关系图或 DGML 关系图（或文档）。 代码图是 DGML 关系图的专用类型。|-   [可视化代码](../modeling/visualize-code.md)<br />-   [Working with Classes and Other Types (Class Designer)](../ide/working-with-classes-and-other-types-class-designer.md)<br />-   [Video: Understand your code dependencies through visualization (Channel 9)](https://go.microsoft.com/fwlink/?LinkID=252065)<br />-   [Video: Visualize the impact of a change (Channel 9)](https://go.microsoft.com/fwlink/?LinkID=252068)|
|**描述和沟通用户需求**：<br /><br /> -   Clarify user stories, business rules, and other requirements and help ensure their consistency by drawing UML diagrams such as use case, activity, and class diagrams.|-   [Create models for your app](../modeling/create-models-for-your-app.md)<br />-   [Model user requirements](../modeling/model-user-requirements.md)<br />-   [Video: Improve architecture through modeling (Channel 9)](https://go.microsoft.com/fwlink/?LinkID=252078)|
|**定义体系结构**：<br /><br /> -   Model the large-scale structure of your software system and the design patterns by drawing UML component, class, and sequence diagrams.<br />-   Define and enforce constraints on dependencies between the components of your code by creating layer diagrams.|-   [Create models for your app](../modeling/create-models-for-your-app.md)<br />-   [Model your app's architecture](../modeling/model-your-app-s-architecture.md)<br />-   [Video: Improve architecture through modeling (Channel 9)](https://go.microsoft.com/fwlink/?LinkID=252078)<br />-   [Video: Use layer diagrams to design and validate your architecture (Channel 9)](https://go.microsoft.com/fwlink/?LinkID=252073)|
|**使用要求和预期设计来验证你的系统：**<br /><br /> -   Define acceptance tests or system tests based on the requirements models. 这将在测试和用户要求之间建立一种稳固的关系，并有助于在要求更改时更轻松地更新系统。<br />-   Validate code dependencies with layer diagrams that describe the intended architecture and prevent changes that might conflict with the design.|-   [Validate your system during development](../modeling/validate-your-system-during-development.md)<br />-   [Video: Use layer diagrams to design and validate your architecture (Channel 9)](https://go.microsoft.com/fwlink/?LinkID=252073)|
|**使用 Team Foundation 版本控制共享模型、关系图和代码图**：<br /><br /> -   Put code maps, modeling projects, UML diagrams, and layer diagrams under Team Foundation version control so you can share them.|当多个用户使用 Team Foundation 版本控制下的这些项时，使用这些指南会有助于避免版本控制问题：<br /><br /> -   [Manage models and diagrams under version control](../modeling/manage-models-and-diagrams-under-version-control.md)|
|**从 UML 或域特定语言生成或配置应用程序的各部分**：<br /><br /> -   Make your design more responsive to requirements changes and easily variable across a product line.|-   [Generate and configure your app from models](../modeling/generate-and-configure-your-app-from-models.md)|
|**自定义模型和关系图**：<br /><br /> -   Adapt models to how your project uses them by defining additional properties for UML elements, validation constraints to make sure that your models conform to your business rules, and additional menu commands and toolbox items.<br />-   Create your own domain-specific languages.|-   [Extend UML models and diagrams](../modeling/extend-uml-models-and-diagrams.md)<br />-   [Modeling SDK for Visual Studio - Domain-Specific Languages](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|
|**使用 T4 模板生成文本**：<br /><br /> -   Use text blocks and control logic inside templates to generate text-based files.|-   [Code Generation and T4 Text Templates](../modeling/code-generation-and-t4-text-templates.md)|

## <a name="types-of-models-and-their-uses"></a>模型类型和用法

|**模型类型和典型用法**|
|-------------------------------------|
|**代码图**<br /><br /> 代码图可帮助查看代码中的组织和关系。<br /><br /> 典型用法：<br /><br /> -   Examine program code so you can better understand its structure and its dependencies, how to update it, and estimate the cost of proposed changes.<br /><br /> 请参阅：<br /><br /> -   [Map dependencies across your solutions](../modeling/map-dependencies-across-your-solutions.md)<br />-   [Use code maps to debug your applications](../modeling/use-code-maps-to-debug-your-applications.md)<br />-   [Find potential problems using code map analyzers](../modeling/find-potential-problems-using-code-map-analyzers.md)|
|**Layer diagram**<br /><br /> 层关系图可将应用程序的结构定义为一组带有显式依赖项的层或块。 可以运行验证来发现代码中依赖项和层关系图中所述依赖项之间的冲突。<br /><br /> 典型用法：<br /><br /> -   Stabilize the structure of the application through numerous changes over its life.<br />-   Discover unintentional dependency conflicts before checking in changes to the code.<br /><br /> 请参阅：<br /><br /> -   [Create layer diagrams from your code](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [Layer Diagrams: Reference](../modeling/layer-diagrams-reference.md)<br />-   [Validate code with layer diagrams](../modeling/validate-code-with-layer-diagrams.md)|
|**UML model**<br /><br /> UML 模型包含多个视图，其中包括类、组件、用例、活动和序列图。 可以自定义 UML 以满足自己的应用程序域。 例如，可以将标记、其他信息和约束附加到模型元素。 还可以定义在模型上操作的工具。 See [Create models for your app](../modeling/create-models-for-your-app.md).<br /><br /> 典型用法：<br /><br /> -   Describe requirements and design. 可以将 UML 快速地应用于任何应用程序的开发中。 See [Use models in your development process](../modeling/use-models-in-your-development-process.md).<br />-   Generate or configure tests or parts of an application. 若要自定义表示法并开发生成模板或可配置应用程序，则需要进行一些工作。 See [Generate and configure your app from models](../modeling/generate-and-configure-your-app-from-models.md).<br />-   For general description and for code generation or configuration in smaller projects.|
|**域特定语言 (DSL)**<br /><br /> DSL 是为特定目的而设计的一种表示法。 在 Visual Studio 中通常表示为图形。<br /><br /> 典型用法：<br /><br /> -   Generate or configure parts of the application. 若要开发表示法和工具，则需要进行工作。 其产生的结果，与 UML 自定义相比，会更好地适应你的域。<br />-   For large projects or in product lines where the investment in developing the DSL and its tools is returned by its use in more than one project.<br /><br /> 请参阅：<br /><br /> -   [Modeling SDK for Visual Studio - Domain-Specific Languages](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|

## <a name="where-can-i-get-more-information"></a>在何处可以获取详细信息？

|||
|-|-|
|**论坛**|-   [Visual Studio 可视化和建模工具](https://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visual Studio 可视化和建模 SDK（DSL 工具）](https://go.microsoft.com/fwlink/?LinkId=184721)|

## <a name="see-also"></a>请参阅

- [What's new for modeling in Visual Studio 2015](../modeling/what-s-new-for-design-in-visual-studio.md)
- [DevOps 和应用程序生命周期管理](https://msdn.microsoft.com/library/74a1f71d-7f23-4c71-8fd7-89ede614fab6)
