---
title: 在生成大型项目时有效使用内存 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- memory use (MSBuild)
- msbuild, efficient memory use building large trees
- caching (MSBuild)
ms.assetid: 853a21ed-69f7-4817-af00-57f73e2c74b5
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 28d9f3d43faa53731b101dfdf58fe1e68a0920c5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68178299"
---
# <a name="using-memory-efficiently-when-you-build-large-projects"></a>在生成大型项目时有效使用内存
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

大型项目通常包含许多子项目和其他依赖项，并且它们可能会在生成时占用大量系统内存。 当可用系统内存减少时，系统性能可能也会降低。 较旧版本的 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 项目保留在内存中，或者 3.5 版中的项目会被删除，但会在缓存中保留生成结果，供将来检索。  
  
 4.0 版会自动处理此内存管理，项目无需使用 `UnloadProjectsOnCompletion` 和 `UseResultsCache` 等属性。  
  
## <a name="see-also"></a>另请参阅  
 [并行生成多个项目](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)
