---
title: Visual Studio 2017 中用于设计的新增功能
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio], architecture and modeling
- architecture [Visual Studio], modeling
- modeling software [Visual Studio], What's New
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
monikerRange: vs-2017
ms.openlocfilehash: 51d4f4d2af5dde398744d926e45200ec16c6214a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72666940"
---
# <a name="whats-new-for-design-in-visual-studio-2017"></a>Visual Studio 2017 中用于设计的新增功能

## <a name="live-dependency-validation"></a>实时依赖项验证

删除不需要的依赖项是管理技术债务的重要部分。 Visual Studio 提供依赖项的实时验证，包括有关问题的精确信息，例如它们所在的位置。 实时依赖项验证在错误列表和编辑器中充分利用新功能。

![操作中的实时依赖项验证](media/dep-validation-whatsnew-01.png)

创作体验已更改，使得依赖项验证更易于发现和更易于访问。 术语已从 "层关系图" 更改为 "依赖关系图"。

"**体系结构**" 菜单现在包含直接创建依赖关系图的命令：

!["体系结构" 菜单上的实时依赖项](media/dep-validation-whatsnew-02.png)

已更改层属性名称和说明，使其更有意义：

![实时依赖项更新属性名称](media/dep-validation-whatsnew-03.png)

每次保存关系图时，都会立即看到解决方案中当前代码的更改所带来的影响。 你不必等待 "**验证依赖项**" 命令的完成。

有关更多详细信息，请参阅[此博客文章](https://devblogs.microsoft.com/devops/live-architecture-dependency-validation-in-visual-studio-15-preview-5/)。

## <a name="uml-designers-have-been-removed"></a>UML 设计器已删除

UML 设计器已从 Visual Studio 中删除。

* UML 关系图现在显示为 XML 文件
* UML 模型资源管理器不再存在
* 建模项目引用不再用于依赖项验证
* 不再显示解决方案资源管理器中的 "层引用" 节点
* 不再使用依赖项（层）关系图上的 "验证" 生成操作-已删除生成任务
* 维护项目结构，以便在不同版本之间进行往返
* 你仍可以打开、创建、编辑和保存作为 XML 的依赖项（层）关系图
* 在设计图面上无法访问链接到依赖项（层）关系图的 TFS 工作项
* 不再支持从到 DSL 或层的反向链接
* 不再支持建模 SDK 中的 UML 扩展性

支持可视化 .NET 和C++代码的体系结构是通过[代码图](map-dependencies-across-your-solutions.md)提供的。

如果你是 UML 设计人员的重要用户，可以继续使用 Visual Studio 2015 或更早版本，同时确定你的 UML 需求的替代工具。

有关更多详细信息，请参阅[此博客文章](https://devblogs.microsoft.com/devops/uml-designers-have-been-removed-layer-designer-now-supports-live-architectural-analysis/)。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="a-nameversionsupport-edition-support-for-architecture-and-modeling-tools"></a>对体系结构和建模工具的 <a name="VersionSupport" />Edition 支持

Visual Studio 提供多种版本。 并非所有这些都提供对体系结构和建模工具的支持。 下表显示每个工具的可用性。

|**功能**|**企业版**|**专业版**|**社区版**|
|-|-|-|-|
|**代码图**|是|仅支持读取代码图，筛选代码映射，添加新的泛型节点，以及通过选择创建新的定向关系图。|-|
|**依赖项关系图**|是|仅支持读取依赖项关系图。|仅支持读取依赖项关系图。|
|**定向关系图**（DGML 关系图）|是|是|是|
|**代码克隆**|是|-|-|