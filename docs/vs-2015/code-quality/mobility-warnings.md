---
title: 移动性警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.MobilityRules
helpviewer_keywords:
- managed code analysis warnings, mobility warnings
- mobility warnings
- warnings, mobility
ms.assetid: 9808054c-593b-4fc3-92cc-1fc45f41569c
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c9f5606540d55c0a2c4257ff397ad77cc55624b4
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655984"
---
# <a name="mobility-warnings"></a>移动性警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

移动性警告支持高效使用电源。

## <a name="in-this-section"></a>本节内容

|规则|描述|
|----------|-----------------|
|[CA1600：不要使用 Idle 进程优先级](../code-quality/ca1600-do-not-use-idle-process-priority.md)|不要将进程优先级设置为 Idle。 具有 System.Diagnostics.ProcessPriorityClass.Idle 优先级的进程将在 CPU 本应处于空闲状态时占用它，从而阻止进入待机状态。|
|[CA1601：不要使用阻止电源状态更改的计时器](../code-quality/ca1601-do-not-use-timers-that-prevent-power-state-changes.md)|频率较高的定期活动会使 CPU 处于繁忙状态，并且会干扰具有节能功能（关闭显示器和硬盘）的空闲计时器。|
