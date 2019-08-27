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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153723"
---
# <a name="operational-modes"></a>操作模式
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

有三种模式在其中 IDE 可以操作，按如下所示：  
  
- [设计模式](#vsconoperationalmodesanchor1)  
  
- [运行模式](#vsconoperationalmodesanchor2)  
  
- [中断模式](#vsconoperationalmodesanchor3)  
  
  如何在自定义调试引擎 (DE) 转换这些模式之间是要求你熟悉转换机制的实施决策。 DE 可能或不能直接实现这些模式。 这些模式是真正调试包模式切换的基于用户执行任何操作或来自德国的事件。 例如，从运行模式下以中断模式的转换被策划从 DE 停止事件。 从中断模式或步骤模式下运行的转换是由用户执行操作，例如步骤或 Execute 策划。 有关 DE 转换的详细信息，请参阅[控制执行](../../extensibility/debugger/control-of-execution.md)。  
  
## <a name="vsconoperationalmodesanchor1"></a> 设计模式  
 设计模式是 nonrunning 状态的 Visual Studio 调试时，在此期间可以设置调试应用程序中的功能。  
  
 仅几个调试过程设计模式中使用的功能。 开发人员可以选择设置断点或创建监视表达式。 DE 永远不会加载或 IDE 处于设计模式时调用。 与 DE 交互运行和中断模式期间发生。  
  
## <a name="vsconoperationalmodesanchor2"></a> 运行模式  
 在 IDE 中调试会话中运行程序时，会发生运行模式。 应用程序运行之前终止，，直到遇到断点，或引发异常。 当应用程序运行时终止，DE 转换到设计模式。 当命中断点或引发异常时，DE 将转换为中断模式。  
  
## <a name="vsconoperationalmodesanchor3"></a> 中断模式  
 调试程序执行的挂起时发生中断模式。 中断模式下提供了开发人员在中断时该应用程序的快照，并允许开发人员可以分析应用程序状态和更改应用程序将运行方式。 开发人员可以查看和编辑代码、 检查或修改数据、 重新启动该应用程序、 结束执行，或继续执行从同一点。  
  
 DE 发送同步停止事件时进入中断模式。 同步停止事件，也称为停止事件通知会话调试管理器 (SDM) 和正在调试的应用程序已停止执行代码的 IDE。 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)并[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)接口是停止事件的示例。  
  
 正在停止事件是通过调用以下方法，转换在调试器中中断模式下才能运行或单步模式之一 （续）：  
  
- [Execute](../../extensibility/debugger/reference/idebugprocess3-execute.md)  
  
- [Step](../../extensibility/debugger/reference/idebugprocess3-step.md)  
  
- [Continue](../../extensibility/debugger/reference/idebugprocess3-continue.md)  
  
### <a name="vsconoperationalmodesanchor4"></a> 步骤模式  
 到下一行代码，或到、 逐过程或函数的程序步骤时发生步执行模式。 通过调用该方法执行某个步骤[步骤](../../extensibility/debugger/reference/idebugprocess3-step.md)。 此方法需要`DWORD`指定的 s [STEPUNIT](../../extensibility/debugger/reference/stepunit.md)并[STEPKIND](../../extensibility/debugger/reference/stepkind.md)枚举作为输入参数。  
  
 如果程序已成功将单步到下一行代码或执行某一函数，或将运行到光标处或设置断点，DE 将自动转换返回到中断模式。  
  
## <a name="see-also"></a>请参阅  
 [控制执行](../../extensibility/debugger/control-of-execution.md)
