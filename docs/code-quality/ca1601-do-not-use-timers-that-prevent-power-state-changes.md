---
title: CA1601:不要使用阻止电源状态更改的计时器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1601
- DoNotUseTimersThatPreventPowerStateChanges
helpviewer_keywords:
- CA1601
- DoNotUseTimersThatPreventPowerStateChanges
ms.assetid: b8028c92-0696-4c54-9773-0028f29bda9a
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1300b733cbd4808359089787ceebeb0750de6723
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234347"
---
# <a name="ca1601-do-not-use-timers-that-prevent-power-state-changes"></a>CA1601:不要使用阻止电源状态更改的计时器

|||
|-|-|
|TypeName|DoNotUseTimersThatPreventPowerStateChanges|
|CheckId|CA1601|
|类别|Microsoft.Mobility|
|重大更改|重大|

## <a name="cause"></a>原因
计时器的间隔设置为每秒出现一次以上。

## <a name="rule-description"></a>规则说明
请不要每秒轮询一次以上，或者使用比每秒一次更频繁的计时器。 频率较高的定期活动会使 CPU 处于繁忙状态，并且会干扰具有节能功能（关闭显示器和硬盘）的空闲计时器。

## <a name="how-to-fix-violations"></a>如何解决冲突
将计时器间隔设置为每秒不到一次。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
仅当每秒触发计时器的时间多于一次并且需要能够安全地忽略移动性注意事项时，才应禁止此规则。