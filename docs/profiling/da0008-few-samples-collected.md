---
title: DA0008：收集的样本过少 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.rules.DATooFewSamples
- vs.performance.8
- vs.performance.DA0008
- vs.performance.rules.DA0008
ms.assetid: 8a5b78aa-7b3d-476c-a47d-abfaff3fae7c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6b33193f30edd19ef18ead5cf15f2e41d352f4d4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62936613"
---
# <a name="da0008-few-samples-collected"></a>DA0008：收集的样本过少

|||
|-|-|
|规则 ID|DA0008|
|类别|分析工具使用情况|
|分析方法|采样|
|消息|仅收集了少量样本。 请考虑运行更长的时间或使用更快的采样率，以获取更有意义的结果。|
|规则类型|信息|

## <a name="cause"></a>原因
 分析运行期间仅收集了少量样本。

## <a name="rule-description"></a>规则说明
 使用采样方法时，应该收集大量具有统计学意义的样本，以确保数据反映实际的程序行为。 为了尽量减少采样错误，应尝试至少收集 1000 个程序指令执行行为的样本。 如果不收集足够的样本，则分析分析数据时可能产生误导。

## <a name="how-to-fix-violations"></a>如何解决冲突
 请考虑分析运行时间较长的应用程序或使用较快的采样速率，以获得具有统计学意义的结果。 有关如何更改 Visual Studio IDE 中的采样速率的信息，请参阅[如何：选择采样事件](../profiling/how-to-choose-sampling-events.md)。 有关使用分析工具命令行时如何更改采样速率的详细信息，请参阅 [VSPerfCmd](../profiling/vsperfcmd.md) 引用中的[计时器](../profiling/timer.md)。