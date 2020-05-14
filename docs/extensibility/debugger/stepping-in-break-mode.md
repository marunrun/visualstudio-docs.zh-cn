---
title: 步入中断模式 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode, stepping
- stepping, in break mode
- debugging [Debugging SDK], stepping in break mode
ms.assetid: b08dc8ee-6c63-4462-a097-6f525cfbb35a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3161fc1c1ec8b44d96b3793198ac630ba2e32d67
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712859"
---
# <a name="stepping-in-break-mode"></a>步进进入中断模式
以下部分介绍调试器处于中断模式且必须单步执行代码时发生的过程：

## <a name="stepping-process"></a>步进过程

1. 调用[IDebugProgram2：：](../../extensibility/debugger/reference/idebugprogram2-step.md)使用[STEPKIND](../../extensibility/debugger/reference/stepkind.md)和[STEPUNIT](../../extensibility/debugger/reference/stepunit.md)参数执行步骤的步骤。

2. 完成此步骤后，将[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)作为停止事件发送。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
