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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840809"
---
# <a name="attaching-after-a-launch"></a>启动后附加
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

启动程序后，调试会话便已准备好将调试引擎附加 (DE) 。  
  
## <a name="design-decisions"></a>设计决策  
 由于通信在共享地址空间内更容易，因此你必须确定是否可以更好地简化调试会话与 DE 之间的通信，或在 DE 与程序之间进行通信。 选择以下各项：  
  
- 如果便于在调试会话与取消之间进行通信，调试会话会创建 DE，并请求取消附加到该程序。 这会使调试会话并将其放在一个地址空间中，同时将运行时环境和程序一起放入另一个地址空间。  
  
- 如果可以更好地简化 DE 与程序之间的通信，则运行时环境将创建 DE。 这将在一个地址空间中保留 SDM，并在另一个地址空间中将其放在一起。 这是使用解释器实现的、用于运行脚本语言的 DE 的典型。  
  
    > [!NOTE]
    > DE 附加到该程序的方式依赖于实现。 DE 与程序之间的通信也依赖于实现。  
  
## <a name="implementation"></a>实现  
 以编程方式，当会话调试管理器 (SDM) 首先收到表示要启动的程序的 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) 对象时，它将调用 [Attach](../../extensibility/debugger/reference/idebugprogram2-attach.md) 方法，并向其传递一个 [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) 对象，该对象稍后用于将调试事件传递回 SDM。 然后，该 `IDebugProgram2::Attach` 方法调用 [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) 方法。 有关 SDM 如何接收接口的详细信息 `IDebugProgram2` ，请参阅 [通知端口](../../extensibility/debugger/notifying-the-port.md)。  
  
 如果您的 DE 需要在与要调试的程序相同的地址空间中运行，通常是由于 DE 是运行脚本的解释器的一部分，因此该 `IDebugProgramNodeAttach2::OnAttach` 方法返回 `S_FALSE` ，指示它已完成附加过程。  
  
 另一方面，如果在 SDM 的地址空间中运行了 DE，则 `IDebugProgramNodeAttach2::OnAttach` 方法返回 `S_OK` 或 [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md) 接口根本不会在与正在调试的程序关联的 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) 对象上实现。 在这种情况下，将最终调用 [attach](../../extensibility/debugger/reference/idebugengine2-attach.md) 方法来完成附加操作。  
  
 在后一种情况下，您必须[GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)对 `IDebugProgram2` 传递给方法的对象调用 GetProgramId 方法 `IDebugEngine2::Attach` ，将存储 `GUID` 在本地程序对象中，并在 `GUID` `IDebugProgram2::GetProgramId` 随后对此对象调用方法时返回此方法。 `GUID`用于跨各种调试组件唯一标识程序。  
  
 请注意，在方法返回的情况下，将用于该程序的将 `IDebugProgramNodeAttach2::OnAttach` `S_FALSE` `GUID` 传递到该方法，并且它是在 `IDebugProgramNodeAttach2::OnAttach` `GUID` 本地程序对象上设置的方法。  
  
 现在已将 DE 附加到节目，并已准备好发送任何启动事件。  
  
## <a name="see-also"></a>另请参阅  
 [直接附加到程序](../../extensibility/debugger/attaching-directly-to-a-program.md)   
 [通知端口](../../extensibility/debugger/notifying-the-port.md)   
 [调试任务](../../extensibility/debugger/debugging-tasks.md)   
 [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)   
 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)   
 [附件](../../extensibility/debugger/reference/idebugprogram2-attach.md)   
 [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)   
 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)   
 [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)   
 [附加](../../extensibility/debugger/reference/idebugengine2-attach.md)
