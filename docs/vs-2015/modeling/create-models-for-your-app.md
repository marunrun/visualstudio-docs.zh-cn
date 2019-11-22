---
title: Create models for your app | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.teamarch.common.commentlink.properties
- vs.teamarch.UMLModelExplorer.dependency
- vs.teamarch.UMLModelExplorer.commentlink
- vs.teamarch.common.dependency.properties
- Microsoft.VisualStudio.Uml.Diagrams.CommentShape.IsTransparent
- vs.teamarch.common.comment.properties
- vs.teamarch.UMLModelExplorer.comment
helpviewer_keywords:
- diagrams - modeling, sequence
- software design
- diagrams - modeling, use case
- diagrams - modeling, component
- diagrams - modeling, UML component
- UML model
- diagrams - modeling, UML use case
- diagrams - modeling, class
- diagrams - modeling, activity
- diagrams - modeling, UML activity
- software modeling
- diagrams - modeling, UML sequence
- UML
- diagrams - modeling, UML
- diagrams - modeling, layer
- software, designing
- diagrams - modeling, UML class
- software, modeling
- UML diagrams
ms.assetid: b69d9d91-c7e7-4dee-8eb6-706076eecb85
caps.latest.revision: 60
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a9f20629c39bc37ca20550c3b88d8ecb2aca470f
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300245"
---
# <a name="create-models-for-your-app"></a>为你的应用程序创建模型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

建模图有助于理解、阐明和传达代码的构思和软件系统必须支持的用户需求。 例如，若要描述和传达用户需求，你可以使用统一建模语言 (UML) 用例图、活动图、类图和序列图。 若要描述和传达系统的功能，你可以使用 UML 组件图、类图、活动图和序列图。

 See [Channel 9 Video: Improve architecture through modeling](https://go.microsoft.com/fwlink/?LinkID=252078).

 在此版本中，可以创建以下 UML 关系图：

|**关系图**|**显示**|
|-----------------|---------------|
|[UML 活动图：参考](../modeling/uml-activity-diagrams-reference.md)|业务流程中操作和参与者之间的工作流|
|[UML 组件图：参考](../modeling/uml-component-diagrams-reference.md)|系统的组件、组件的接口、端口和关系|
|[UML 类图：参考](../modeling/uml-class-diagrams-reference.md)|用于在系统中存储和交换数据的类型及其关系|
|[UML 序列图：参考](../modeling/uml-sequence-diagrams-reference.md)|对象、组件、系统或参与者之间的交互序列|
|[UML 用例图：参考](../modeling/uml-use-case-diagrams-reference.md)|系统支持的用户目标和任务|

 To see which versions of Visual Studio support each type of diagram, see [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

 若要可视化系统的体系结构或现有代码，请创建以下关系图：

|**关系图**|**显示**|
|-----------------|---------------|
|[层关系图：指南](../modeling/layer-diagrams-guidelines.md)<br /><br /> [层关系图：参考](../modeling/layer-diagrams-reference.md)|系统的上层体系结构|
|代码图<br /><br /> [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)<br /><br /> [使用代码图分析查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)|现有代码中的依赖关系和其他关系|
|代码生成的类图<br /><br /> [使用类图（类设计器）](../ide/working-with-class-diagrams-class-designer.md)|.NET 代码中的类型及其关系|

## <a name="common-tasks"></a>常规任务

|**Topic**|**Task**|
|---------------|--------------|
|[创建 UML 建模项目和关系图](../modeling/create-uml-modeling-projects-and-diagrams.md)|**Create models** and add diagrams.|
|[编辑 UML 模型和关系图](../modeling/edit-uml-models-and-diagrams.md)|**Draw diagrams** to edit the model.|
|[定义包和命名空间](../modeling/define-packages-and-namespaces.md)|**Create packages** to divide a model into units that different team members can work on.|
|[从 UML 类图生成代码](../modeling/generate-code-from-uml-class-diagrams.md)|**Generate C# code from class diagrams** to start your implementation.|
|[使用配置文件和构造型自定义模型](../modeling/customize-your-model-with-profiles-and-stereotypes.md)|**Customize model elements** using stereotypes, to extend the standard UML model elements for specific purposes.|
|[链接模型元素和工作项](../modeling/link-model-elements-and-work-items.md)|**Create links between model elements and work items** to help you track tasks, test cases, bugs, requirements, issues, or other kinds of work that are associated with specific parts of your model.|
|[将关系图导出为图像](../modeling/export-diagrams-as-images.md)|**Save your model and diagrams** so that you can share them with other users, including those who do not use [!INCLUDE[vsUltShort](../includes/vsultshort-md.md)].|

## <a name="related-tasks"></a>相关任务

|**Topic**|**Task**|
|---------------|--------------|
|[代码可视化](../modeling/visualize-code.md)|创建代码图和层关系图以更好地了解不熟悉的代码。|
|[建立用户需求模型](../modeling/model-user-requirements.md)|使用模型来阐明和传达用户的需求。|
|[应用体系结构建模](../modeling/model-your-app-s-architecture.md)|使用模型来描述系统的整体结构和行为，并确保它满足用户的需求。|
|[在开发过程中验证系统](../modeling/validate-your-system-during-development.md)|确保软件与用户的需求和系统的整体体系结构保持一致。|
|[在你的开发过程中使用模型](../modeling/use-models-in-your-development-process.md)<br /><br /> [Use models in Agile development](https://msdn.microsoft.com/592ac27c-3d3e-454a-9c38-b76658ed137f)|使用模型来帮助你在系统开发的过程中了解和更改你的系统。|
|[安排建模解决方案](../modeling/structure-your-modeling-solution.md)|在大中型项目中组织模型。|

## <a name="external-resources"></a>外部资源

|**类别**|**Links**|
|------------------|---------------|
|**论坛**|-   [Visual Studio 可视化和建模工具](https://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visual Studio 可视化和建模 SDK（DSL 工具）](https://go.microsoft.com/fwlink/?LinkId=184721)|
