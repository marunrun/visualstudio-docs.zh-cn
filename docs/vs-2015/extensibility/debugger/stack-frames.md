---
title: 堆栈帧 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- stack frames, debugging
- debugging [Debugging SDK], stack frames
- stack frames
ms.assetid: b5e439d4-1e9d-4e13-9cad-bb8b136d4ca8
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d3050e89db2f5cbb138f3d358b10c7cd936c560e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62423382"
---
# <a name="stack-frames"></a>堆栈帧
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在调试器体系结构，方面**堆栈帧**:  
  
- 是提供一个线程的执行上下文堆栈的抽象。 函数内始终执行线程。 堆栈帧保存到它的函数和参数的本地变量。 若要使用 Visual Studio 进行调试，语言或正在调试的环境必须支持堆栈帧。  
  
- 可以同时标识和描述自身，并可以返回关联的线程。 表示当前指令指针，并将相关的文档的代码上下文和表达式计算上下文，还可以返回一个堆栈帧。  
  
- 具有名称、 类型和值的本地变量和参数，用于描述和它在各种 IDE 调试窗口中显示的属性。  
  
- 为由[IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)接口，通常创建的调试引擎 (DE) 或虚拟机，因此执行线程。  
  
## <a name="see-also"></a>请参阅  
 [调试器上下文](../../extensibility/debugger/debugger-contexts.md)   
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)   
 [调试引擎](../../extensibility/debugger/debug-engine.md)   
 [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)
