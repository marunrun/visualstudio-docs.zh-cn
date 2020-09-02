---
title: 操作模式 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, modes
ms.assetid: f69972d0-809d-40df-9da3-04738791391c
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c4009ab6268140117c8fd1294adcc52ac347b799
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153723"
---
# <a name="operational-modes"></a>操作模式
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

IDE 可在三种模式下运行，如下所示：  
  
- [设计模式](#vsconoperationalmodesanchor1)  
  
- [运行模式](#vsconoperationalmodesanchor2)  
  
- [中断模式](#vsconoperationalmodesanchor3)  
  
  自定义调试引擎 (如何在这些模式间取消) 转换是一种实现决策，要求你熟悉过渡机制。 DE 可能会也可能不会直接实现这些模式。 这些模式实际上是调试包模式，可基于用户操作或从取消的事件切换。 例如，从运行模式到中断模式的转换是从 DE 停止事件策划的。 用户执行操作（例如单步执行或执行）时，从中断过渡到运行模式或单步执行模式的转换是策划的。 有关取消转换的详细信息，请参阅 [控制执行](../../extensibility/debugger/control-of-execution.md)。  
  
## <a name="design-mode"></a><a name="vsconoperationalmodesanchor1"></a> 设计模式  
 设计模式是 Visual Studio 调试的 nonrunning 状态，在这种情况下，你可以在应用程序中设置调试功能。  
  
 设计模式期间只使用少量的调试功能。 开发人员可以选择设置断点或创建监视表达式。 IDE 处于设计模式时，不会加载或调用 DE。 与 DE 的交互发生在运行和中断模式下。  
  
## <a name="run-mode"></a><a name="vsconoperationalmodesanchor2"></a> 运行模式  
 当程序在 IDE 的调试会话中运行时，将发生运行模式。 应用程序在终止之前运行，直到命中断点，或直到引发异常为止。 当应用程序运行终止时，将转换为设计模式。 命中断点或引发异常时，取消转换为中断模式。  
  
## <a name="break-mode"></a><a name="vsconoperationalmodesanchor3"></a> 中断模式  
 当调试程序的执行挂起时，中断模式发生。 中断模式为开发人员提供应用程序在中断时的快照，并使开发人员能够分析应用程序的状态，并更改应用程序的运行方式。 开发人员可以查看和编辑代码、检查或修改数据、重新启动应用程序、结束执行或从同一点继续执行。  
  
 当 DE 发送同步停止事件时，将进入中断模式。 同步停止事件（也称为停止事件）通知会话调试管理器 (SDM) 和 IDE 中正在调试的应用程序已停止执行代码。 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)和[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)接口是停止事件的示例。  
  
 停止事件的方法是：调用以下方法之一，将调试器从中断模式转换为运行或单步执行模式：  
  
- [执行](../../extensibility/debugger/reference/idebugprocess3-execute.md)  
  
- [步骤](../../extensibility/debugger/reference/idebugprocess3-step.md)  
  
- [继续](../../extensibility/debugger/reference/idebugprocess3-continue.md)  
  
### <a name="step-mode"></a><a name="vsconoperationalmodesanchor4"></a> 单步执行模式  
 步骤模式发生于程序执行下一行代码时，或单步执行、逐过程执行或跳出函数。 步骤通过调用方法 [步骤](../../extensibility/debugger/reference/idebugprocess3-step.md)来执行。 此方法需要 `DWORD` 将 [STEPUNIT](../../extensibility/debugger/reference/stepunit.md) 和 [STEPKIND](../../extensibility/debugger/reference/stepkind.md) 枚举指定为输入参数。  
  
 当程序成功地执行下一行代码或进入函数时，或者运行到游标或设置断点时，将自动转换回中断模式。  
  
## <a name="see-also"></a>另请参阅  
 [控制执行](../../extensibility/debugger/control-of-execution.md)
