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
ms.openlocfilehash: 1055136562d59412a6187524dc6023c55ef2dc3c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68158660"
---
# <a name="da0010-expensive-gethashcode"></a>DA0010：高开销 GetHashCode
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 的最新文档，请参阅[DA0010:高开销 GetHashCode](https://docs.microsoft.com/visualstudio/profiling/da0010-expensive-gethashcode)。  

|||  
|-|-|  
|规则 ID|DA0010|  
|类别|.NET Framework 使用情况|  
|分析方法|采样<br /><br /> .NET 内存|  
|消息|GetHashCode 函数成本应较低，且不应分配任何内存。 如果可能，降低哈希代码函数的复杂性。|  
|消息类型|警告|  
  
## <a name="cause"></a>原因  
 对该类型的 GetHashCode 方法的调用在分析数据中占很大比例或此方法分配内存。  
  
## <a name="rule-description"></a>规则说明  
 哈希是一项用于快速定位大型集合中的某个特定项的技术。 由于哈希表可以变得非常大，并且必须支持的访问率高，哈希表应非常有效。 此要求的含义是 .NET Framework 中的 GetHashCode 方法不应分配内存。 分配内存会增加垃圾回收器上的负载，并向潜在延迟公开该方法（如果因分配请求而需要运行垃圾回收）。  
  
## <a name="how-to-fix-violations"></a>如何解决冲突  
 降低方法的复杂性。
