---
title: MSBuild 最佳做法 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
helpviewer_keywords:
- best practices, MSBuild
- MSBuild, best practices
ms.assetid: 90ef8693-e921-410a-a377-fe4d13f58c48
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e597b10913ad495193545ab304b3b324d8f66b41
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68181114"
---
# <a name="msbuild-best-practices"></a>MSBuild 最佳做法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

我们建议下列编写 MSBuild 脚本的最佳做法：  
  
- 默认属性值的最佳处理方式是使用 `Condition` 特性，而不是声明可在命令行中重写其默认值的属性。 例如，使用  
  
     `<MyProperty Condition="$(MyProperty)" == ''>`  
  
     `MyDefaultValue`  
  
     `</MyProperty>`  
  
- 在选择项目时，请避免使用通配符。 而应显式指定文件。 这使得跟踪在添加或删除文件时可能出现的错误更加简单。  
  
## <a name="see-also"></a>另请参阅  
 [高级概念](../msbuild/msbuild-advanced-concepts.md)
