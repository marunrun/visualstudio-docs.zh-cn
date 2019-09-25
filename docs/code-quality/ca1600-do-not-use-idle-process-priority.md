---
title: CA1600:不要使用 Idle 进程优先级
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DoNotUseIdleProcessPriority
- CA1600
helpviewer_keywords:
- CA1600
- DoNotUseIdleProcessPriority
ms.assetid: 9b0d073b-78b6-41be-8ef3-14692a735283
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 686929471ee8b6b5d1896f61bcbcd97a59135462
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234368"
---
# <a name="ca1600-do-not-use-idle-process-priority"></a>CA1600:不要使用 Idle 进程优先级

|||
|-|-|
|TypeName|DoNotUseIdleProcessPriority|
|CheckId|CA1600|
|类别|Microsoft.Mobility|
|重大更改|重大|

## <a name="cause"></a>原因
当进程设置为时， `ProcessPriorityClass.Idle`将出现此规则。

## <a name="rule-description"></a>规则说明
不要将进程优先级设置为 Idle。 如果进程在其他情况下处于空闲状态，则会占用CPU，因而会阻止待机。`System.Diagnostics.ProcessPriorityClass.Idle`

## <a name="how-to-fix-violations"></a>如何解决冲突
将进程设置`ProcessPriorityClass.BelowNormal`为。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
仅当需要空闲进程优先级时才应禁止显示此规则，并且可以安全地忽略移动性注意事项。