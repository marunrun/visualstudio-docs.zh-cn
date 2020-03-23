---
title: Visual Studio 2017 中用于设计的新增功能
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio], architecture and modeling
- architecture [Visual Studio], modeling
- modeling software [Visual Studio], What's New
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
monikerRange: vs-2017
ms.openlocfilehash: 6f81cc32604abe6d90ac0d263574e97df35c63bd
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301493"
---
# <a name="whats-new-for-design-in-visual-studio-2017"></a>Visual Studio 2017 中用于设计的新增功能

## <a name="live-dependency-validation"></a>实时依赖项验证

删除不需要的依赖项是管理技术债务的一个重要部分。 Visual Studio 提供依赖项的实时验证，包括有关问题（如问题位于何处）的准确信息。 实时依赖项验证充分利用了错误列表和编辑器中的新功能。

![实时依赖项验证在操作中](media/dep-validation-whatsnew-01.png)

创作体验已更改，使依赖项验证更易于发现和更易于访问。 术语从"层图"更改为"依赖关系图"。

**体系结构**菜单现在包含直接创建依赖关系关系图的命令：

![体系结构菜单上的实时依赖项项](media/dep-validation-whatsnew-02.png)

图层属性名称和说明已更改，使其更有意义：

![实时依赖项更新的属性名称](media/dep-validation-whatsnew-03.png)

每次保存关系图时，您都会立即看到解决方案中当前代码的分析结果中更改的影响。 您不必等待**验证依赖项**命令的完成。

有关更多详细信息，请参阅[这篇博客文章](https://devblogs.microsoft.com/devops/live-architecture-dependency-validation-in-visual-studio-15-preview-5/)。

## <a name="uml-designers-have-been-removed"></a>UML 设计器已被删除

UML 设计器已从可视化工作室中删除。

* UML 关系图现在作为 XML 文件显示
* UML 模型资源管理器不再存在
* 建模项目引用不再用于依赖项验证
* 解决方案资源管理器中的"图层引用"节点不再显示
* 不再使用依赖项（层）关系图上的"验证"生成操作 - 已删除生成任务
* 项目结构维护，用于在版本之间往返
* 您仍然可以打开、创建、编辑和保存依赖项（层）关系图作为 XML
* 链接到依赖项（层）图的 TFS 工作项在设计图上不可访问
* 不再支持从 DSL 或图层进行回链接
* 建模 SDK 中的 UML 可扩展性不再受支持

可通过[代码映射](map-dependencies-across-your-solutions.md)支持可视化 .NET 和C++代码的体系结构。

如果您是 UML 设计人员的重要用户，则可以在决定满足 UML 需求的替代工具时继续使用 Visual Studio 2015 或更早版本。

有关更多详细信息，请参阅[这篇博客文章](https://devblogs.microsoft.com/devops/uml-designers-have-been-removed-layer-designer-now-supports-live-architectural-analysis/)。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="edition-support-for-architecture-and-modeling-tools"></a><a name="VersionSupport" />对体系结构和建模工具的版式支持

Visual Studio 有多种版本版本。 并非所有这些都为体系结构和建模工具提供支持。 下表显示每个工具的可用性。

|**功能**|**企业版**|**专业版**|**社区版**|
|-|-|-|-|
|**代码映射**|是|仅支持读取代码映射、筛选代码映射、添加新的泛型节点以及从所选内容创建新的定向图。|-|
|**依赖关系图**|是|仅支持读取依赖关系关系图。|仅支持读取依赖关系关系图。|
|**定向图**（DGML 图表）|是|是|是|
|**代码克隆**|是|-|-|
