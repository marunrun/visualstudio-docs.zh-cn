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
ms.openlocfilehash: c37affc585653807912d00c1cfe365853fd6260b
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921809"
---
# <a name="ca1600-do-not-use-idle-process-priority"></a>CA1600:不要使用 Idle 进程优先级

|||
|-|-|
|TypeName|DoNotUseIdleProcessPriority|
|CheckId|CA1600|
|类别|Microsoft.Mobility|
|是否重大更改|重大|

## <a name="cause"></a>原因
当进程设置为时, `ProcessPriorityClass.Idle`将出现此规则。

## <a name="rule-description"></a>规则说明
不要将进程优先级设置为 Idle。 如果进程在其他情况下处于空闲状态, 则会占用CPU,因而会阻止待机。`System.Diagnostics.ProcessPriorityClass.Idle`

## <a name="how-to-fix-violations"></a>如何解决冲突
将进程设置`ProcessPriorityClass.BelowNormal`为。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
仅当需要空闲进程优先级时才应禁止显示此规则, 并且可以安全地忽略移动性注意事项。