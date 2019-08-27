---
title: CA1600:不要使用 idle 进程优先级 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 4002e17e3988ca3b449e141394ce762f95ffc78b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68189297"
---
# <a name="ca1600-do-not-use-idle-process-priority"></a>CA1600:不要使用 Idle 进程优先级
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotUseIdleProcessPriority|
|CheckId|CA1600|
|类别|Microsoft.Mobility|
|是否重大更改|重大|

## <a name="cause"></a>原因
 当进程设置为时将引发此规则`ProcessPriorityClass.Idle`。

## <a name="rule-description"></a>规则说明
 不要将进程优先级设置为 Idle。 进程`System.Diagnostics.ProcessPriorityClass.Idle`它本应处于空闲状态，并因此将阻止进入待机状态时占用 CPU。

## <a name="how-to-fix-violations"></a>如何解决冲突
 设置为进程`ProcessPriorityClass.BelowNormal`。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 仅当 Idle 进程优先级是必需的且可以安全地忽略移动性注意事项时，应禁止显示此规则。
