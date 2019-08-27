---
title: DA0011：高开销的 CompareTo | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.DA0011
- vs.performance.rules.DAExpensiveCompareTo
- vs.performance.11
- vs.performance.rules.DA0011
ms.assetid: 239a381d-0d97-4367-8668-746c93f5af2c
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 86d41a2717eb3ef7bd49f8d34b85198a55e5101c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68158650"
---
# <a name="da0011-expensive-compareto"></a>DA0011：高开销 CompareTo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 的最新文档，请参阅[DA0011:高开销的 CompareTo](https://docs.microsoft.com/visualstudio/profiling/da0011-expensive-compareto)。  
  
|||  
|-|-|  
|规则 ID|DA0011|  
|类别|.NET Framework 使用情况|  
|分析方法|采样<br /><br /> .NET 内存|  
|消息|CompareTo 函数应该比较便宜，且不应分配任何内存。 如果可能，降低 CompareTo 函数的复杂性。|  
|规则类型|警告|  
  
## <a name="cause"></a>原因  
 类型的 CompareTo 方法开销巨大或分配内存。  
  
## <a name="rule-description"></a>规则说明  
 CompareTo 方法应高效，且不应分配内存。  
  
## <a name="how-to-fix-violations"></a>如何解决冲突  
 降低 CompareTo 方法的复杂性。
