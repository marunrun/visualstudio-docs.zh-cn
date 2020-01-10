---
title: 可视化代码 |Microsoft Docs
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
ms.openlocfilehash: 9dcb6edf8ce69d48805c3ad8c3c25ef9cc0ed591
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75851348"
---
# <a name="visualize-code"></a>可视化代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以在 Visual Studio 中使用可视化和建模工具，以帮助你了解现有代码并描述你的应用程序。 这可以让你直观地了解更改可能对代码产生的影响，并帮助你评估更改导致的工作和风险。 例如：

- 了解代码的关系，可以用可视的方式映射这些关系。

- 若要描述你的系统体系结构并确保代码与其设计保持一致，创建层关系图并对这些关系图进行代码验证。

- 若要描述类结构，请创建类关系图。

- 为系统的各个方面建模并进行沟通，绘制统一建模语言 (UML) 关系图。 例如，你可以为系统组件、类型、交互和进程建模。

  这些工具还可以帮助你更轻松地与参与项目的人员进行沟通。 例如，你可以使用 UML 类关系图创建用于与项目利益干系人、用户和团队成员讨论系统的常用词汇表。

  若要查看支持每个功能的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)

## <a name="what-do-you-want-to-do"></a>要执行什么操作Јї

|||
|-|-|
|**了解代码及其关系：**<br /><br /> 特定代码段之间的代码图关系<br /><br /> 请参阅整个解决方案中的代码关系概述。<br /><br /> **注意**：在此版本的 Visual Studio 中，术语 *代码图* 用于替换 *依赖项关系图*。|-   [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)<br />-   [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)<br />-   [使用代码图分析器查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)<br />[调试时 -   调用堆栈上的映射方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)|
|**了解类结构：**<br /><br /> 通过从代码创建类关系图，在项目中查看类的结构。|[如何：向项目中添加类图（类设计器）](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)|
|**描述高级系统设计并根据此设计验证代码：**<br /><br /> 通过创建层关系图，描述高级系统设计及其预期的依赖项。 对此设计进行代码验证，以确保代码中的依赖项与设计保持一致。|-   [从代码创建层关系图](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [层关系图：参考](../modeling/layer-diagrams-reference.md)<br />-   [层关系图：准则](../modeling/layer-diagrams-guidelines.md)<br />-   [用层关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)|
|**传达用户需求和体系结构：**<br /><br /> 通过绘制以下 UML 关系图：活动、组件、类、序列和用例，建立用户需求和软件系统体系结构模型。|-   [为应用创建模型](../modeling/create-models-for-your-app.md)<br />-   [模型用户需求](../modeling/model-user-requirements.md)<br />-   [应用程序体系结构的模型](../modeling/model-your-app-s-architecture.md)|

## <a name="external-resources"></a>外部資源

|**类别**|**Links**|
|------------------|---------------|
|**论坛**|-   [Visual Studio 可视化和建模工具](https://social.msdn.microsoft.com/Forums/en-US/home?forum=vsarch)<br />-   [Visual Studio 可视化和建模 SDK（DSL 工具）](https://social.msdn.microsoft.com/Forums/home?forum=dslvsarchx)|
|**Blogs**|[Visual Studio ALM + Team Foundation Server 博客](https://blogs.msdn.com/b/visualstudioalm)|
|**技术文章和日志**|[MSDN 体系结构论坛](https://msdn.microsoft.com/architecture/default.aspx)|

## <a name="see-also"></a>请参阅
 [方案：使用可视化和建模](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)[分析和建模体系结构](../modeling/analyze-and-model-your-architecture.md)[来更改设计为应用模型创建模型](../modeling/create-models-for-your-app.md)[用户需求](../modeling/model-user-requirements.md)[模型应用体系结构](../modeling/model-your-app-s-architecture.md)[在开发过程中使用模型](../modeling/use-models-in-your-development-process.md)
