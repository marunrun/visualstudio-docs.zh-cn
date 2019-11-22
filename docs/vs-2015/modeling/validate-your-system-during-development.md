---
title: Validate your system during development | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- layer diagrams
ms.assetid: c9dafb47-7b1d-4c72-9432-d43be3db1799
caps.latest.revision: 39
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4fec3595ba7886f5ba979c35e9441ab108174726
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301336"
---
# <a name="validate-your-system-during-development"></a>在开发过程中验证系统
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 可帮助使你的软件与用户的要求和系统的体系结构保持一致。

 若要查看支持各个功能的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="key-tasks"></a>关键任务
 使用以下任务来验证软件。

|**任务**|**相关主题**|
|---------------|---------------------------|
|**Make sure your model is consistent:**<br /><br /> 由于项目使用和解释模型方式会有所不同，因此禁用某些元素组合可能会有所帮助。 例如，可以限制 UML 类，以使它们始终具有符合 [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)]的名称。 你可以以这些方式在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展中定义约束。|-   [Validate your UML model](../modeling/validate-your-uml-model.md)<br />-   [Define validation constraints for UML models](../modeling/define-validation-constraints-for-uml-models.md)|
|**请确保软件满足用户要求**：<br /><br /> 可以使用要求模型和体系结构模型来帮助组织系统及其组件的测试。 这种做法有助于确保你测试了对于用户和其他利益干系人而言非常重要的要求，并可帮助你在要求发生变化时快速更新测试。|-   [Develop tests from a model](../modeling/develop-tests-from-a-model.md)|
|**请确保你的软件与系统的预期设计保持一致：**<br /><br /> 层关系图描述了应用程序组件之间的预期依赖关系。 在开发期间，你可以验证代码中的实际依赖关系是否符合预期设计。|-   [Create layer diagrams from your code](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [Validate code with layer diagrams](../modeling/validate-code-with-layer-diagrams.md)|

## <a name="external-resources"></a>外部资源

|**类别**|**Links**|
|------------------|---------------|
|**视频**|![link to video](../data-tools/media/playvideo.gif "PlayVideo") [Channel 9: Doug Seven: Code Understanding and System Design with Visual Studio 2010](https://go.microsoft.com/fwlink/?LinkId=216100)<br /><br /> ![link to video](../data-tools/media/playvideo.gif "PlayVideo") [Channel 9: Architecting an Application using a Layer Diagram](https://go.microsoft.com/fwlink/?LinkID=201117)<br /><br /> ![link to video](../data-tools/media/playvideo.gif "PlayVideo") [MSDN How Do I Series: How to Validate Code using Layer Diagrams](https://go.microsoft.com/fwlink/?LinkID=214405)|
|**论坛**|-   [Visual Studio 可视化和建模工具](https://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visual Studio 可视化和建模 SDK（DSL 工具）](https://go.microsoft.com/fwlink/?LinkId=184721)|
|**Blogs**|-   [Visual Studio ALM + Team Foundation Server 博客](https://go.microsoft.com/fwlink/?LinkID=201340)|
|**技术文章和日志**|[MSDN 体系结构中心](https://go.microsoft.com/fwlink/?LinkId=201343)|

## <a name="see-also"></a>请参阅
 [Testing the application](https://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac) [Extend UML models and diagrams](../modeling/extend-uml-models-and-diagrams.md) [Model user requirements](../modeling/model-user-requirements.md) [Analyzing and Modeling Architecture](../modeling/analyze-and-model-your-architecture.md)
