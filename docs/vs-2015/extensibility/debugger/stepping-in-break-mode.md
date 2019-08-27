---
title: 在中断模式中单步执行 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- break mode, stepping
- stepping, in break mode
- debugging [Debugging SDK], stepping in break mode
ms.assetid: b08dc8ee-6c63-4462-a097-6f525cfbb35a
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 482d7131692c1e22483c80f4b4bb22e07a6caf1a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62423356"
---
# <a name="stepping-in-break-mode"></a>步入中断模式
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

下面介绍调试器处于中断模式下，必须单步执行代码时发生的过程：  
  
## <a name="stepping-process"></a>单步执行过程  
  
1. 调用[IDebugProgram2::Step](../../extensibility/debugger/reference/idebugprogram2-step.md)与[STEPKIND](../../extensibility/debugger/reference/stepkind.md)并[STEPUNIT](../../extensibility/debugger/reference/stepunit.md)自变量执行的步骤。  
  
2. 完成步骤后，发送[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)为停止事件。  
  
## <a name="see-also"></a>请参阅  
 [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
