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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 2d5803544e4e7279179929c7c04a3792e4dd9318
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68183865"
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
  
## <a name="what-do-you-want-to-do"></a>你希望做什么？  
  
|||  
|-|-|  
|**了解代码和其关系：**<br /><br /> 特定代码段之间的代码图关系<br /><br /> 请参阅整个解决方案中的代码关系概述。<br /><br /> **说明**：在此版本的 Visual Studio 中，术语*代码图*用来代替*依赖项关系图*。|-   [映射解决方案之间的依赖项](../modeling/map-dependencies-across-your-solutions.md)<br />-   [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)<br />-   [使用代码图分析器发现潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)<br />-   [调试时映射调用堆栈上的方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)|  
|**了解类结构：**<br /><br /> 通过从代码创建类关系图，在项目中查看类的结构。|[如何：向项目添加类图（类设计器）](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)|  
|**描述高级系统设计和验证对此设计的代码：**<br /><br /> 通过创建层关系图，描述高级系统设计及其预期的依赖项。 对此设计进行代码验证，以确保代码中的依赖项与设计保持一致。|-   [从代码创建层关系图](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [层关系图：引用](../modeling/layer-diagrams-reference.md)<br />-   [层关系图：指南](../modeling/layer-diagrams-guidelines.md)<br />-   [使用层关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)|  
|**沟通用户需求和体系结构：**<br /><br /> 通过绘制以下 UML 关系图：活动、组件、类、序列和用例，建立用户需求和软件系统体系结构模型。|-   [为您的应用程序创建模型](../modeling/create-models-for-your-app.md)<br />-   [建立用户需求模型](../modeling/model-user-requirements.md)<br />-   [应用程序的体系结构建模](../modeling/model-your-app-s-architecture.md)|  
  
## <a name="external-resources"></a>外部资源  
  
|**类别**|**Links**|  
|------------------|---------------|  
|**论坛**|-   [Visual Studio 可视化和建模工具](http://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visual Studio 可视化和建模 SDK（DSL 工具）](http://go.microsoft.com/fwlink/?LinkId=184721)|  
|**博客**|[Visual Studio ALM + Team Foundation Server 博客](http://go.microsoft.com/fwlink/?LinkID=201340)|  
|**技术文章和日志**|[MSDN 体系结构论坛](http://go.microsoft.com/fwlink/?LinkId=201343)|  
  
## <a name="see-also"></a>请参阅  
 [场景：使用可视化和建模更改设计](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)   
 [分析体系结构和建模](../modeling/analyze-and-model-your-architecture.md)   
 [为您的应用程序创建模型](../modeling/create-models-for-your-app.md)   
 [建立用户需求模型](../modeling/model-user-requirements.md)   
 [应用程序的体系结构建模](../modeling/model-your-app-s-architecture.md)   
 [在你的开发过程中使用模型](../modeling/use-models-in-your-development-process.md)
