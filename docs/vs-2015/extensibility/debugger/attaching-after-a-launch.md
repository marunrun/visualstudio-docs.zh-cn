---
title: 启动后附加 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 5a3600a1-dc20-4e55-b2a4-809736a6ae65
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 693cf6d746f51862415f2f30e46d48a998047f14
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63437439"
---
# <a name="attaching-after-a-launch"></a>启动后附加
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

启动程序后，调试会话已准备好附加到上述程序的调试引擎 (DE)。  
  
## <a name="design-decisions"></a>设计决策  
 因为通信更容易共享的地址空间内，您必须决定是否更有意义以便于调试会话和德国，DE 和程序之间或之间的通信。 在以下选择：  
  
- 如果它更有意义便于调试会话和 DE 之间进行通信，调试会话共同创建 DE，并询问 DE 将附加到该程序。 这使调试会话，DE 一起中一个地址空间的运行时环境和程序中另一个合并在一起。  
  
- 如果它更有意义便于 DE 与程序之间进行通信，运行时环境将共同创建 DE。 这将使一个地址空间中的 SDM DE、 运行时环境和程序中另一个合并在一起。 这是典型的部署使用解释器以运行脚本化的语言实现。  
  
    > [!NOTE]
    > 如何将 DE 附加到该程序是依赖于实现的。 DE 和程序之间的通信也是依赖于实现的。  
  
## <a name="implementation"></a>实现  
 以编程方式，当会话调试管理器 (SDM) 首次收到[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)对象，该对象表示要启动的程序，它将调用[附加](../../extensibility/debugger/reference/idebugprogram2-attach.md)方法，并向其传递[IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)对象，它是更高版本用于传递回 SDM 调试事件。 `IDebugProgram2::Attach`方法随后调用[OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)方法。 有关详细信息如何 SDM 接收`IDebugProgram2`接口，请参阅[通知端口](../../extensibility/debugger/notifying-the-port.md)。  
  
 如果需要为正在调试的程序，通常因为 DE 是运行一个脚本，解释器的一部分的相同地址空间中运行你 DE`IDebugProgramNodeAttach2::OnAttach`方法将返回`S_FALSE`，指示它已附加过程完成。  
  
 如果手动，DE 在 SDM，地址空间中运行`IDebugProgramNodeAttach2::OnAttach`方法将返回`S_OK`或[IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)上根本不实现接口[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)与正在调试的程序关联的对象。 在这种情况下，[附加](../../extensibility/debugger/reference/idebugengine2-attach.md)方法最终调用以完成附加操作。  
  
 在后一种情况下，必须调用[GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)方法`IDebugProgram2`对象传递给`IDebugEngine2::Attach`方法、 应用商店`GUID`本地程序中对象，并返回此`GUID`时`IDebugProgram2::GetProgramId`随后对此对象调用方法。 `GUID`用于在各种调试组件之间唯一地标识该程序。  
  
 请注意的情况下`IDebugProgramNodeAttach2::OnAttach`方法返回`S_FALSE`，则`GUID`要用于该程序将传递给该方法，并且`IDebugProgramNodeAttach2::OnAttach`方法以设置`GUID`上的本地程序对象。  
  
 DE 现在已附加到程序中并准备好发送任何启动事件。  
  
## <a name="see-also"></a>请参阅  
 [直接附加到程序](../../extensibility/debugger/attaching-directly-to-a-program.md)   
 [通知端口](../../extensibility/debugger/notifying-the-port.md)   
 [调试任务](../../extensibility/debugger/debugging-tasks.md)   
 [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)   
 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)   
 [附加](../../extensibility/debugger/reference/idebugprogram2-attach.md)   
 [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)   
 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)   
 [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)   
 [附加](../../extensibility/debugger/reference/idebugengine2-attach.md)
