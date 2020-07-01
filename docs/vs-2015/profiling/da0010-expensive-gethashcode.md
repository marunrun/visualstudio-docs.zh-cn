---
title: DA0010：高开销 GetHashCode | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.rules.DAExpensiveGetHashCode
- vs.performance.DA0010
- vs.performance.rules.DA0010
- vs.performance.10
ms.assetid: 3987e21a-5b4f-45e4-8a33-6b3f0a472c08
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: af234cd130d06c2a76c5ddbc958a67eb064d9128
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547571"
---
# <a name="da0010-expensive-gethashcode"></a>DA0010：高开销 GetHashCode
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有关 Visual Studio 的最新文档，请参阅[DA0010：昂贵的 GetHashCode](/visualstudio/profiling/da0010-expensive-gethashcode)。  

|Item|值|  
|-|-|  
|规则 ID|DA0010|  
|Category|.NET Framework 使用情况|  
|分析方法|采样<br /><br /> .NET 内存|  
|消息|GetHashCode 函数成本应较低，且不应分配任何内存。 如果可能，降低哈希代码函数的复杂性。|  
|消息类型|警告|  
  
## <a name="cause"></a>原因  
 对该类型的 GetHashCode 方法的调用在分析数据中占很大比例或此方法分配内存。  
  
## <a name="rule-description"></a>规则描述  
 哈希是一项用于快速定位大型集合中的某个特定项的技术。 由于哈希表可能非常大，并且必须支持高访问速率，因此哈希表应该非常高效。 此要求的含义是 .NET Framework 中的 GetHashCode 方法不应分配内存。 分配内存会增加垃圾回收器上的负载，并向潜在延迟公开该方法（如果因分配请求而需要运行垃圾回收）。  
  
## <a name="how-to-fix-violations"></a>如何解决冲突  
 降低方法的复杂性。
