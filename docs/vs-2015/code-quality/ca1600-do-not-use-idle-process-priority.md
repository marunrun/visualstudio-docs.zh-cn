---
title: CA1600：不使用空闲进程优先级 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotUseIdleProcessPriority
- CA1600
helpviewer_keywords:
- CA1600
- DoNotUseIdleProcessPriority
ms.assetid: 9b0d073b-78b6-41be-8ef3-14692a735283
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 3f6233136dcf7f1db5d622a02419d33e0eedacf5
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545673"
---
# <a name="ca1600-do-not-use-idle-process-priority"></a>CA1600:不要使用 Idle 进程优先级
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|DoNotUseIdleProcessPriority|
|CheckId|CA1600|
|类别|Microsoft. 移动性|
|是否重大更改|重大|

## <a name="cause"></a>原因
 当进程设置为时，将出现此规则 `ProcessPriorityClass.Idle` 。

## <a name="rule-description"></a>规则描述
 不要将进程优先级设置为 Idle。 如果进程在 `System.Diagnostics.ProcessPriorityClass.Idle` 其他情况下处于空闲状态，则会占用 CPU，因而会阻止待机。

## <a name="how-to-fix-violations"></a>如何解决冲突
 将进程设置为 `ProcessPriorityClass.BelowNormal` 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 仅当需要空闲进程优先级时才应禁止显示此规则，并且可以安全地忽略移动性注意事项。
