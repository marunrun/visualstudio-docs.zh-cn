---
title: 在中断模式中单步执行 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode, stepping
- stepping, in break mode
- debugging [Debugging SDK], stepping in break mode
ms.assetid: b08dc8ee-6c63-4462-a097-6f525cfbb35a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e3a8688f32a97d27ee6f6e2d18fcea8e25feaac2
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348549"
---
# <a name="stepping-in-break-mode"></a>在中断模式下单步执行
以下部分介绍调试器处于中断模式，并且必须单步执行代码时发生的过程：

## <a name="stepping-process"></a>单步执行过程

1. 调用[IDebugProgram2::Step](../../extensibility/debugger/reference/idebugprogram2-step.md)与[STEPKIND](../../extensibility/debugger/reference/stepkind.md)并[STEPUNIT](../../extensibility/debugger/reference/stepunit.md)自变量执行的步骤。

2. 完成步骤后，发送[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)为停止事件。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)