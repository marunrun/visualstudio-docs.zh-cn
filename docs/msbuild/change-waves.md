---
title: 更改波次
description: 了解如何启用或禁用 MSBuild 中潜在的颠覆性功能。
ms.date: 11/10/2020
ms.topic: conceptual
helpviewer_keywords:
- Change waves [MSBuild]
- MSBuildDisableFeaturesFromVersion environment variable
author: ghogen
ms.author: ghogen
manager: jillfra
monikerRange: '>=vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: 68aafd8ebb97b4bf649cc41eb7739e1700c9cb1a
ms.sourcegitcommit: 83a39d48b00c6c351e5c1707942633b7f73aaad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2020
ms.locfileid: "94545662"
---
# <a name="change-waves"></a>更改波次

变更波是 MSBuild 中的一组行为变更，你可以通过指定特定标志作为环境变量来选择停用。 这样做的目的是警告你潜在的颠覆性更改，以便你可以在这些更改成为标准功能前灵活地适应它们。 特定变更波中的所有功能只能一起启用或禁用，而不能单独启用或禁用。

当你升级到新版 MSBuild 时，潜在的颠覆性更改是默认启用的，但如果某项功能对你的生成产生负面影响，你可以轻松地禁用相应变更波。 每个变更波都由 MSBuild 版本号（例如 16.8）标识，但设置变更波只控制某些可能影响生成过程的功能，而不是相应 MSBuild 版本中的所有更改。 [本文稍后的部分中](#change-waves-and-associated-features)列出了每个变更波中的功能。 禁用一个变更波也会禁用更高版本的变更波。

## <a name="opt-out-of-change-wave-features"></a>选择停用变更波功能

若要禁用变更波中的功能，请将环境变量 `MSBuildDisableFeaturesFromVersion` 设置为包含要禁用的功能的变更波（或 MSBuild 版本）。 这是为其开发功能的 MSBuild 的版本。 请参阅下面的变更波与功能的映射。

### <a name="msbuilddisablefeaturesfromversion-values"></a>MSBuildDisableFeaturesFromVersion 值

如果你没有将 `MSBuildDisableFeaturesFromVersion` 设置为有效的变更波，则会收到警告和/或默认为特定变更波。 下表显示了可能的设置：

| `MSBuildDisableFeaturesFromVersion` 值                         | 结果        | 收到警告？ |
| :-------------                                                    | :----------   | :----------: |
| 取消设置                                                             | 启用所有变更波，这意味着每个变更波后面的所有功能都被启用。               | 否   |
| 任何有效的当前变更波（例如 `16.8`）                      | 禁用变更波 `16.8` 及更高版本后面的所有功能。                                           | 否   |
| 无效值（例如，如果有效波为 `16.8` 和 `16.10`，则为 `16.9`）| 默认为最接近的有效值（升序）。 例如，如果设置 `16.9`，则默认为 `16.10`。               | 否   |
| 不轮换（例如，如果最高波为 `17.0`，则为 `17.1`）      | 固定为最接近的有效值。 例如，`17.1` 固定为 `17.0`，`16.5` 固定为 `16.8`                    | 是  |
| 无效格式（例如 `16x8`、`17_0`、`garbage`）                    | 启用所有变更波，这意味着每个变更波后面的所有功能都被启用。               | 是  |

## <a name="change-waves-and-associated-features"></a>变更波和关联的功能

下面列表中的链接指向功能的 GitHub PR。

### <a name="168"></a>16.8

- [启用 NoWarn](https://github.com/dotnet/msbuild/pull/5671)
- [将目标/任务跳过的日志消息截断为 1024 个字符](https://github.com/dotnet/msbuild/pull/5553)
- [不要在 false 条件下展开全驱动器 glob](https://github.com/dotnet/msbuild/pull/5669)

### <a name="1610"></a>16.10

- [当条件中的属性展开有空格时出错](https://github.com/dotnet/msbuild/pull/5672)

### <a name="170"></a>17.0

此变更波中还没有任何条目。

## <a name="change-waves-that-are-out-of-rotation"></a>不轮换的变更波

目前没有不轮换的变更波。

## <a name="faq"></a>FAQ

**为什么要每隔一个地定位版本来轮换变更波？**

我们认为，有足够的时间与受影响的人进行讨论，并协助适应这些更改。

**为什么是环境变量，而不是项目属性？**

在某些情况下，我们希望在 MSBuild 加载项目之前，将功能置于变更波下。 因此，变更波需要使用环境变量。

**为什么是选择停用，而不是选择启用？**

选择停用对我们来说是一种更好的方法，否则当某项功能影响客户的生成时，我们可能会得到有限的反馈。

## <a name="see-also"></a>另请参阅

- [MSBuild](msbuild.md)
- [MSBuild 16 中的新变化](whats-new-msbuild-16-0.md)
