---
title: Visual Studio 2017 中用于设计的新增功能
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio], architecture and modeling
- architecture [Visual Studio], modeling
- modeling software [Visual Studio], What's New
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
monikerRange: vs-2017
ms.openlocfilehash: dc75c7414e0fff18f76d14f8f9a4e0779a9e7a2b
ms.sourcegitcommit: 6a19c5ece38a70731496a38f2ef20676ff18f8a4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476539"
---
# <a name="whats-new-for-design-in-visual-studio-2017"></a>Visual Studio 2017 中用于设计的新增功能

## <a name="live-dependency-validation"></a>实时依赖项验证

删除不需要的依赖项是管理技术债务的重要组成部分。 Visual Studio 提供依赖项，包括有关的问题，如的位置的精确信息的实时的验证。 实时依赖项验证采用完整的优点错误列表和在编辑器中的新增功能。

![操作中的实时依赖项验证](media/dep-validation-whatsnew-01.png)

创作体验已更改为更容易地发现、 更易于访问使依赖项验证。 术语已从"层关系图"更改为"依赖项关系图"。

**体系结构**菜单现在包含直接创建依赖项关系图的命令：

![实时依赖项的体系结构菜单项](media/dep-validation-whatsnew-02.png)

已更改层的属性名称和说明，以使其更有意义：

![更新的实时依赖项属性名称](media/dep-validation-whatsnew-03.png)

您立即看到在解决方案中的当前代码分析结果中的更改的影响每次保存关系图。 无需等待完成**验证依赖关系**命令。

有关更多详细信息，请参阅[这篇博客文章](https://devblogs.microsoft.com/devops/live-architecture-dependency-validation-in-visual-studio-15-preview-5/)。

## <a name="uml-designers-have-been-removed"></a>已删除 UML 设计器

UML 设计器已从 Visual Studio 中删除。

* UML 关系图现在显示为 XML 文件
* UML 模型资源管理器不再存在
* 建模的项目引用不能再用于依赖项验证
* 不再显示在解决方案资源管理器中的"层引用"节点
* 不再使用依赖项 （层） 关系图上的"验证"生成操作-已删除生成任务
* 为版本之间的往返维护项目结构
* 您可以仍打开、 创建、 编辑和将依赖项 （层） 关系图另存为 XML
* TFS 工作项链接到依赖项 （层） 关系图不能访问在设计图面上
* 不再支持后从链接到 DSL 或图层
* 不再支持 UML 建模 SDK 的可扩展性

支持用于可视化的.NET 体系结构和C++代码是可通过[代码映射](map-dependencies-across-your-solutions.md)。

如果您是 UML 设计器的大量用户，你可以继续使用 Visual Studio 2015 或更早版本，而 UML 需要确定一种备选工具。

有关更多详细信息，请参阅[这篇博客文章](https://devblogs.microsoft.com/devops/uml-designers-have-been-removed-layer-designer-now-supports-live-architectural-analysis/)。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="a-nameversionsupport-edition-support-for-architecture-and-modeling-tools"></a><a name="VersionSupport" />对体系结构和建模工具的版本支持

Visual Studio 有多个版本。 并非所有这些体系结构和建模工具提供支持。 下表显示每个工具的可用性。

|**功能**|**企业版**|**专业版**|**社区版**|
|-|-|-|-|
|**代码图**|是|仅支持读取代码图，筛选代码映射时，添加新的泛型节点和从所选内容创建新的定向关系图。|-|
|**依赖项关系图**|是|仅支持读取依赖项关系图。|仅支持读取依赖项关系图。|
|**定向关系图**（DGML 关系图）|是|是|是|
|**代码克隆**|是|-|-|