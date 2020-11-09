---
title: 在生成大型项目时有效使用内存 | Microsoft Docs
description: 了解 MSBuild 如何在生成大型项目时自动管理内存，如卸载旧版本和检索缓存。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- memory use (MSBuild)
- msbuild, efficient memory use building large trees
- caching (MSBuild)
ms.assetid: 853a21ed-69f7-4817-af00-57f73e2c74b5
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 61bfa09bf91b49c163e47bbf71c0d192b6950160
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93047613"
---
# <a name="use-memory-efficiently-when-you-build-large-projects"></a>在生成大型项目时有效使用内存

大型项目通常包含许多子项目和其他依赖项，它们可能会在生成时占用大量系统内存。 当可用系统内存减少时，系统性能可能也会降低。 旧版本的 MSBuild 项目保留在内存中。 版本 3.5 删除了项目的旧版本，但在缓存中保留了生成结果以供将来检索。

 4.0 版会自动处理此内存管理，项目无需使用 `UnloadProjectsOnCompletion` 和 `UseResultsCache` 等属性。

### <a name="see-also"></a>另请参阅

- [并行生成多个项目](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)
