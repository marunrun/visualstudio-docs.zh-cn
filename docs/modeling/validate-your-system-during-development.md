---
title: 在开发过程中验证系统
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- dependency diagrams
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ae2b7d81b1f166e6cc97debc3291661d59ee6960
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594027"
---
# <a name="validate-your-system-during-development"></a>在开发过程中验证系统

Visual Studio 可帮助使你的软件与用户的要求和系统的体系结构保持一致。

若要查看支持各个功能的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="key-tasks"></a>关键任务

使用以下任务来验证软件：

|**任务**|**相关主题**|
|-|-|
|**请确保软件满足用户要求**：<br /><br />使用要求和体系结构模型来帮助组织系统及其组件的测试。 这种做法有助于确保你测试了对于用户和其他利益干系人而言非常重要的要求，并可帮助你在要求发生变化时快速更新测试。|- [从模型开发测试](../modeling/develop-tests-from-a-model.md)|
|**请确保你的软件与系统的预期设计保持一致：**<br /><br />依赖关系图描述了应用程序组件之间的预期依赖关系。 在开发期间，你可以验证代码中的实际依赖关系是否符合预期设计。|- [从代码创建依赖项关系图](../modeling/create-layer-diagrams-from-your-code.md)<br />- [通过依赖关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)|

## <a name="external-resources"></a>外部資源

|**类别**|**Links**|
|-|-|
|**视频**|![链接到视频](../data-tools/media/playvideo.gif) 第[9 频道： Doug 7：代码理解和 Visual Studio 2010 的系统设计](https://channel9.msdn.com/shows/VS2010Launch/Doug-Seven-Code-Understanding-and-Systems-Design-with-Visual-Studio-2010)<br /><br /> ![链接到视频](../data-tools/media/playvideo.gif) 第[9 频道：构造应用程序](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-5-architecting-an-application)）|
|**论坛**|- [Visual Studio 可视化和建模工具](https://social.msdn.microsoft.com/Forums/en-US/home?forum=vsarch)<br />- [Visual Studio 扩展性](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vsx)|

## <a name="see-also"></a>另请参阅

- [建立用户需求模型](../modeling/model-user-requirements.md)
- [分析和模型体系结构](../modeling/analyze-and-model-your-architecture.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
