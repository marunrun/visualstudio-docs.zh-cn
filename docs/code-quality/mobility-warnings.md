---
title: Mobility Warnings
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.MobilityRules
helpviewer_keywords:
- managed code analysis warnings, mobility warnings
- mobility warnings
- warnings, mobility
ms.assetid: 9808054c-593b-4fc3-92cc-1fc45f41569c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6061b614442d7bcb2f3465b1c40f35d583626c45
ms.sourcegitcommit: 1efb6b219ade7c35068b79fbdc573a8771ac608d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78167580"
---
# <a name="mobility-warnings"></a>Mobility Warnings
移动性警告支持高效使用电源。

## <a name="in-this-section"></a>本节内容

|规则|说明|
|----------|-----------------|
|[CA1600：不要使用 Idle 进程优先级](../code-quality/ca1600.md)|不要将进程优先级设置为 Idle。 具有 System.Diagnostics.ProcessPriorityClass.Idle 优先级的进程将在 CPU 本应处于空闲状态时占用它，从而阻止进入待机状态。|
|[CA1601：不要使用阻止电源状态更改的计时器](../code-quality/ca1601.md)|频率较高的定期活动会使 CPU 处于繁忙状态，并且会干扰具有节能功能（关闭显示器和硬盘）的空闲计时器。|
