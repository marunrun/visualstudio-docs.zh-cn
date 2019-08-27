---
title: DA0502：所分析的进程的 CPU 最大消耗量 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.rules.DA0502
- vs.performance.DA0502
- vs.performance.502
ms.assetid: 1ee53df5-b0dc-4265-9d4f-527830d08725
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a47a9c5964ccf15d2c609233eb600f39bc3ad2d1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205927"
---
# <a name="da0502-maximum-cpu-consumption-by-the-process-being-profiled"></a>DA0502：所分析的进程的 CPU 最大消耗量
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

规则 Id |DA0502 |  
|类别 |资源监视 |  
|分析方法 |所有 |  
|消息 |此规则仅供参考。 Process()\\% 处理器时间计数器测量正在分析的进程的 CPU 消耗量。 报告的值是在所有测量时间间隔内观察到的最大值。|  
|规则类型 |信息性 |  
  
 使用采样法、.NET 内存或资源争用方法进行分析时，必须收集至少 10 个样本才能触发此规则。  
  
## <a name="rule-description"></a>规则说明  
 此消息报告处理器忙于执行应用程序指令的时间的最大百分比。 报告的值是所分析的进程在其中处于活动状态的所有测量间隔中报告的最大值。 具有多个处理器的计算机上的百分比可能大于 100%。  
  
## <a name="how-to-use-the-rule-data"></a>如何使用规则数据  
 若要了解不同分析方案中应用程序的性能，可使用规则值比较不同版本程序的性能。
