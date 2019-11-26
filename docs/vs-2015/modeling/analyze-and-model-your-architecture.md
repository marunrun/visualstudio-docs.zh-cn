---
title: 分析和建模您的体系结构 |Microsoft Docs
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

 作为开发过程的一部分，可以跨整个应用程序生命周期创建不同详细信息级别的模型。 可通过将模型元素链接到 Team Foundation Server 工作项和开发计划来跟踪要求、任务、测试用例、Bug 和其他与模型关联的工作。 请参阅[方案：使用可视化和建模更改设计](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)。

 若要查看支持每个功能的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)

## <a name="to"></a>到

|||
|-|-|
|**可视化代码**：<br /><br /> -通过创建代码图来查看代码的组织和关系。 可视化程序集、命名空间、类、方法等之间的依赖关系。<br />-通过从代码创建类关系图，查看特定项目的类结构和成员。<br />-通过创建层关系图来验证代码，查找代码和其设计之间的冲突。<br /><br /> **注意**：在此版本的 Visual Studio 中，术语 *代码图* 用于替换 *依赖项关系图*。 术语 *关系图* 在独立使用时，一般指定向关系图或 DGML 关系图（或文档）。 代码图是 DGML 关系图的专用类型。|-   [可视化代码](../modeling/visualize-code.md)<br />[使用类和其他类型的 -   （类设计器）](../ide/working-with-classes-and-other-types-class-designer.md)<br />-   [视频：通过可视化了解代码依赖项（第9频道）](https://go.microsoft.com/fwlink/?LinkID=252065)<br />-   [视频：将更改的影响可视化（通道9）](https://go.microsoft.com/fwlink/?LinkID=252068)|
|**描述和沟通用户需求**：<br /><br /> -阐明用户情景、业务规则和其他要求，并通过绘制 UML 关系图（如用例、活动和类关系图）来帮助确保其一致性。|-   [为应用创建模型](../modeling/create-models-for-your-app.md)<br />-   [模型用户需求](../modeling/model-user-requirements.md)<br />-   [视频：通过建模改善体系结构（第9频道）](https://go.microsoft.com/fwlink/?LinkID=252078)|
|**定义体系结构**：<br /><br /> -通过绘制 UML 组件、类和序列图，对软件系统的大规模结构和设计模式建模。<br />-通过创建层关系图来定义和强制实施代码组件之间依赖关系的约束。|-   [为应用创建模型](../modeling/create-models-for-your-app.md)<br />-   [应用程序体系结构的模型](../modeling/model-your-app-s-architecture.md)<br />-   [视频：通过建模改善体系结构（第9频道）](https://go.microsoft.com/fwlink/?LinkID=252078)<br />-   [视频：使用层关系图设计和验证体系结构（第9频道）](https://go.microsoft.com/fwlink/?LinkID=252073)|
|**使用要求和预期设计来验证你的系统：**<br /><br /> -基于要求模型定义验收测试或系统测试。 这将在测试和用户要求之间建立一种稳固的关系，并有助于在要求更改时更轻松地更新系统。<br />-验证具有描述预期体系结构的层关系图的代码依赖关系，并防止可能与设计发生冲突的更改。|-   [在开发过程中验证系统](../modeling/validate-your-system-during-development.md)<br />-   [视频：使用层关系图设计和验证体系结构（第9频道）](https://go.microsoft.com/fwlink/?LinkID=252073)|
|**使用 Team Foundation 版本控制共享模型、关系图和代码图**：<br /><br /> -将代码图、建模项目、UML 关系图和层关系图置于 Team Foundation 版本控制下，以便可以共享它们。|当多个用户使用 Team Foundation 版本控制下的这些项时，使用这些指南会有助于避免版本控制问题：<br /><br /> -   [管理版本控制下的模型和关系图](../modeling/manage-models-and-diagrams-under-version-control.md)|
|**从 UML 或域特定语言生成或配置应用程序的各部分**：<br /><br /> -使你的设计能够更快地响应需求，并在产品系列之间轻松变化。|-   [从模型生成和配置应用](../modeling/generate-and-configure-your-app-from-models.md)|
|**自定义模型和关系图**：<br /><br /> -通过定义 UML 元素的其他属性、验证约束以确保模型符合业务规则、附加菜单命令和工具箱项，使模型适应项目使用这些模型的方式。<br />-创建您自己的域特定语言。|-   [扩展 UML 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)<br />[适用于 Visual Studio 的 -   建模 SDK-特定于域的语言](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|
|**使用 T4 模板生成文本**：<br /><br /> -使用模板内的文本块和控制逻辑生成基于文本的文件。|-   [代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)|

## <a name="types-of-models-and-their-uses"></a>模型类型和用法

|**模型类型和典型用法**|
|-------------------------------------|
|**代码图**<br /><br /> 代码图可帮助查看代码中的组织和关系。<br /><br /> 典型用法：<br /><br /> -检查程序代码，以便您可以更好地了解其结构及其依赖项，以及如何对其进行更新，并估计建议更改的成本。<br /><br /> 请参阅：<br /><br /> -   [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)<br />-   [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)<br />-   [使用代码图分析器查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)|
|**层关系图**<br /><br /> 层关系图可将应用程序的结构定义为一组带有显式依赖项的层或块。 可以运行验证来发现代码中依赖项和层关系图中所述依赖项之间的冲突。<br /><br /> 典型用法：<br /><br /> -在应用程序的整个生命周期内进行大量更改，从而稳定应用程序的结构。<br />-在将更改签入代码之前发现无意的依赖项冲突。<br /><br /> 请参阅：<br /><br /> -   [从代码创建层关系图](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [层关系图：参考](../modeling/layer-diagrams-reference.md)<br />-   [用层关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)|
|**UML 模型**<br /><br /> UML 模型包含多个视图，其中包括类、组件、用例、活动和序列图。 可以自定义 UML 以满足自己的应用程序域。 例如，可以将标记、其他信息和约束附加到模型元素。 还可以定义在模型上操作的工具。 请参阅[创建应用模型](../modeling/create-models-for-your-app.md)。<br /><br /> 典型用法：<br /><br /> -描述要求和设计。 可以将 UML 快速地应用于任何应用程序的开发中。 请参阅[在开发过程中使用模型](../modeling/use-models-in-your-development-process.md)。<br />-生成或配置应用程序的测试或部件。 若要自定义表示法并开发生成模板或可配置应用程序，则需要进行一些工作。 请参阅[从模型生成和配置应用](../modeling/generate-and-configure-your-app-from-models.md)。<br />-对于较小项目中的常规说明和代码生成或配置。|
|**域特定语言 (DSL)**<br /><br /> DSL 是为特定目的而设计的一种表示法。 在 Visual Studio 中通常表示为图形。<br /><br /> 典型用法：<br /><br /> -生成或配置应用程序的各个部分。 若要开发表示法和工具，则需要进行工作。 其产生的结果，与 UML 自定义相比，会更好地适应你的域。<br />-适用于大项目或产品系列，其中在多个项目中使用它来开发 DSL 及其工具的投资。<br /><br /> 请参阅：<br /><br /> [适用于 Visual Studio 的 -   建模 SDK-特定于域的语言](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|

## <a name="where-can-i-get-more-information"></a>在何处可以获取详细信息？

|||
|-|-|
|**论坛**|-   [Visual Studio 可视化和建模工具](https://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visual Studio 可视化和建模 SDK（DSL 工具）](https://go.microsoft.com/fwlink/?LinkId=184721)|

## <a name="see-also"></a>请参阅

- [Visual Studio 2015 中建模的新增功能](../modeling/what-s-new-for-design-in-visual-studio.md)
- [DevOps 和应用程序生命周期管理](https://msdn.microsoft.com/library/74a1f71d-7f23-4c71-8fd7-89ede614fab6)
