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
ms.openlocfilehash: d4260db808d9c50f78388cf6ba976f7ace52e6a3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669300"
---
# <a name="ca1600-do-not-use-idle-process-priority"></a>CA1600：不要使用 Idle 进程优先级
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotUseIdleProcessPriority|
|CheckId|CA1600|
|类别|Microsoft. 移动性|
|是否重大更改|重大|

## <a name="cause"></a>原因
 当进程设置为 `ProcessPriorityClass.Idle` 时，将出现此规则。

## <a name="rule-description"></a>规则说明
 不要将进程优先级设置为 Idle。 具有 `System.Diagnostics.ProcessPriorityClass.Idle` 的进程将在 CPU 处于空闲状态时占用 CPU，因而会阻止待机。

## <a name="how-to-fix-violations"></a>如何解决冲突
 将进程设置为 `ProcessPriorityClass.BelowNormal`。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 仅当需要空闲进程优先级时才应禁止显示此规则，并且可以安全地忽略移动性注意事项。
