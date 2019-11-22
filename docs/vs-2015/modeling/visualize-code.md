---
title: Visualize code | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- code, understanding
- code, visualizing
- code, exploring
ms.assetid: 0dd7d438-393a-4cd3-b417-9bf37379e1b0
caps.latest.revision: 49
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 955103b6d28e90321fb45c23825f0c2a25362208
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301317"
---
# <a name="visualize-code"></a>可视化代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以在 Visual Studio 中使用可视化和建模工具，以帮助你了解现有代码并描述你的应用程序。 这可以让你直观地了解更改可能对代码产生的影响，并帮助你评估更改导致的工作和风险。 例如:

- 了解代码的关系，可以用可视的方式映射这些关系。

- 若要描述你的系统体系结构并确保代码与其设计保持一致，创建层关系图并对这些关系图进行代码验证。

- 若要描述类结构，请创建类关系图。

- 为系统的各个方面建模并进行沟通，绘制统一建模语言 (UML) 关系图。 例如，你可以为系统组件、类型、交互和进程建模。

  这些工具还可以帮助你更轻松地与参与项目的人员进行沟通。 例如，你可以使用 UML 类关系图创建用于与项目利益干系人、用户和团队成员讨论系统的常用词汇表。

  若要查看支持每个功能的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)

## <a name="what-do-you-want-to-do"></a>你希望做什么？

|||
|-|-|
|**Understand code and its relationships:**<br /><br /> 特定代码段之间的代码图关系<br /><br /> 请参阅整个解决方案中的代码关系概述。<br /><br /> **注意**：在此版本的 Visual Studio 中，术语 *代码图* 用于替换 *依赖项关系图*。|-   [Map dependencies across your solutions](../modeling/map-dependencies-across-your-solutions.md)<br />-   [Use code maps to debug your applications](../modeling/use-code-maps-to-debug-your-applications.md)<br />-   [Find potential problems using code map analyzers](../modeling/find-potential-problems-using-code-map-analyzers.md)<br />-   [Map methods on the call stack while debugging](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)|
|**Understand class structures:**<br /><br /> 通过从代码创建类关系图，在项目中查看类的结构。|[如何：向项目中添加类图（类设计器）](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)|
|**Describe the high-level system design and validate code against this design:**<br /><br /> 通过创建层关系图，描述高级系统设计及其预期的依赖项。 对此设计进行代码验证，以确保代码中的依赖项与设计保持一致。|-   [Create layer diagrams from your code](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [Layer Diagrams: Reference](../modeling/layer-diagrams-reference.md)<br />-   [Layer Diagrams: Guidelines](../modeling/layer-diagrams-guidelines.md)<br />-   [Validate code with layer diagrams](../modeling/validate-code-with-layer-diagrams.md)|
|**Communicate the user requirements and architecture:**<br /><br /> 通过绘制以下 UML 关系图：活动、组件、类、序列和用例，建立用户需求和软件系统体系结构模型。|-   [Create models for your app](../modeling/create-models-for-your-app.md)<br />-   [Model user requirements](../modeling/model-user-requirements.md)<br />-   [Model your app's architecture](../modeling/model-your-app-s-architecture.md)|

## <a name="external-resources"></a>外部资源

|**类别**|**Links**|
|------------------|---------------|
|**论坛**|-   [Visual Studio 可视化和建模工具](https://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visual Studio 可视化和建模 SDK（DSL 工具）](https://go.microsoft.com/fwlink/?LinkId=184721)|
|**Blogs**|[Visual Studio ALM + Team Foundation Server 博客](https://go.microsoft.com/fwlink/?LinkID=201340)|
|**技术文章和日志**|[MSDN Architecture Forum](https://go.microsoft.com/fwlink/?LinkId=201343)|

## <a name="see-also"></a>请参阅
 [Scenario: Change your design using visualization and modeling](../modeling/scenario-change-your-design-using-visualization-and-modeling.md) [Analyzing and Modeling Architecture](../modeling/analyze-and-model-your-architecture.md) [Create models for your app](../modeling/create-models-for-your-app.md) [Model user requirements](../modeling/model-user-requirements.md) [Model your app's architecture](../modeling/model-your-app-s-architecture.md) [Use models in your development process](../modeling/use-models-in-your-development-process.md)
