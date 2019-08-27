---
title: 在生成大型项目时有效使用内存 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- memory use (MSBuild)
- msbuild, efficient memory use building large trees
- caching (MSBuild)
ms.assetid: 853a21ed-69f7-4817-af00-57f73e2c74b5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ab3be342f31e5df018c14f84d30febd38c31c401
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786201"
---
# <a name="use-memory-efficiently-when-you-build-large-projects"></a>在生成大型项目时有效使用内存
大型项目通常包含许多子项目和其他依赖项，它们可能会在生成时占用大量系统内存。 当可用系统内存减少时，系统性能可能也会降低。 旧版本的 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 项目保留在内存中。 版本 3.5 删除了项目的旧版本，但在缓存中保留了生成结果以供将来检索。

 4.0 版会自动处理此内存管理，项目无需使用 `UnloadProjectsOnCompletion` 和 `UseResultsCache` 等属性。

### <a name="see-also"></a>请参阅
- [并行生成多个项目](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)