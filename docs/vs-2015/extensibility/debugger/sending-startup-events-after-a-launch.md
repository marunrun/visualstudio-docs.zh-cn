---
title: 启动后发送启动事件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], startup events
ms.assetid: 306ea0b4-6d9e-4871-8d8d-a4032d422940
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: caf36e6713e49bb1470cd720ba2d04f689abba43
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840532"
---
# <a name="sending-startup-events-after-a-launch"></a>启动后发送启动事件
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

调试引擎 (DE) 附加到程序后，它会向调试会话发送一系列启动事件。  
  
 发回到调试会话的启动事件包括：  
  
- 引擎创建事件。  
  
- 程序创建事件。  
  
- 线程创建和模块加载事件。  
  
- 加载完成事件，在代码加载并准备好运行，但在执行任何代码之前发送  
  
  > [!NOTE]
  > 继续此事件时，将初始化全局变量，并运行启动例程。  
  
- 可能的其他线程创建和模块加载事件。  
  
- 入口点事件，该事件指示程序已到达其主入口点，如 **main** 或 `WinMain` 。 如果将 DE 附加到已在运行的程序，通常不会发送此事件。  
  
  在编程中，取消第一次将会话调试管理器 (SDM 发送) 一个 [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) 接口，该接口表示一个引擎创建事件，后跟一个 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)，表示一个程序创建事件。  
  
  这通常后跟一个或多个 [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) 线程创建事件和 [IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md) 模块加载事件。  
  
  当代码已加载并准备好运行，但在执行任何代码之前，DE 将发送 SDM a [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) load 完成事件。 最后，如果程序尚未运行，则 DE 将发送 [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) 入口点事件，并发出信号表明程序已到达其主入口点并已准备好进行调试。  
  
## <a name="see-also"></a>另请参阅  
 [控制执行](../../extensibility/debugger/control-of-execution.md)   
 [调试任务](../../extensibility/debugger/debugging-tasks.md)
