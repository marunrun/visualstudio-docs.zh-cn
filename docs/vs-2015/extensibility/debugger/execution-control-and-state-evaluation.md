---
title: 执行控件和状态计算 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], execution control
- expression evaluation, control of execution
ms.assetid: 55adde38-1622-4b51-83cb-ce1b04c1ca7a
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bc6476c925f37d70ab45bae129a8b8a379ee519c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152774"
---
# <a name="execution-control-and-state-evaluation"></a>执行控件和状态计算
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

调试应用程序需要实现此类执行控制功能，以单步执行函数，在断点处停止，继续执行。 Visual Studio 调试使其执行控制依赖于在调试器组件之间发送的事件。  
  
## <a name="in-this-section"></a>本节内容  
 [程序控制](../../extensibility/debugger/program-control.md)  
 列出在程序级别发生的以下例程：设置下一个语句、执行、单步执行、继续、挂起和恢复。  
  
 [断点相关的方法](../../extensibility/debugger/breakpoint-related-methods.md)  
 定义 Visual Studio 支持的绑定和挂起的断点类型。  
  
 [调用堆栈计算](../../extensibility/debugger/call-stack-evaluation.md)  
 讨论在中断模式下允许查看调用堆栈堆栈帧的方法的实现。  
  
 [表达式计算](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md)  
 说明如何在分析和评估在 IDE 的某个 windows 中输入的表达式时，调试引擎 (DE) 、表达式计算 (EE) 和会话调试管理器。  
  
 [控件事件](../../extensibility/debugger/control-events.md)  
 讨论在程序的受控执行过程中用于发送事件的接口。
