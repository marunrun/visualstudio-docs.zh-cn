---
title: 线程 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], threads
- threading [Debugging SDK]
ms.assetid: 2243d24a-c3d2-41d1-abbb-6db21a2db9ee
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 028ad25495ba01d9763c8bec3bbb9c4480d72ff8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68185363"
---
# <a name="threads"></a>线程数
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

就调试器体系结构而言， **线程**如下：  
  
- 是计算的基本单位。 线程按顺序在单个调用堆栈的上下文中执行其说明，并从一个代码上下文移到下一个调用堆栈。  
  
- 可以标识自身及其正在其上运行的程序，并且可以命名、挂起和恢复。 线程还可以枚举其关联的堆栈帧，并且在某些情况下，可以将其移动到另一个堆栈帧。 给定堆栈帧的上下文，线程可以返回其关联的逻辑线程（如果有）。 线程具有可在 IDE 的 "线程" 窗口中显示的属性，例如挂起计数。  
  
- 由 [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md) 接口表示，此接口通常由调试引擎创建 (取消) 或虚拟机作为执行程序的结果。  
  
## <a name="see-also"></a>另请参阅  
 [程序](../../extensibility/debugger/programs.md)   
 [堆栈帧](../../extensibility/debugger/stack-frames.md)   
 [调试引擎](../../extensibility/debugger/debug-engine.md)   
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)   
 [会话调试管理器](../../extensibility/debugger/session-debug-manager.md)
