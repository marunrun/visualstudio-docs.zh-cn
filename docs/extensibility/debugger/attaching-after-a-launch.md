---
title: 启动后附加 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 5a3600a1-dc20-4e55-b2a4-809736a6ae65
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3a4ce0a7465891035b43bbb8f6f22f0c064d104c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739281"
---
# <a name="attach-after-a-launch"></a>启动后附加
在程序启动后，调试会话已准备好将调试引擎附加 (DE) 。

## <a name="design-decisions"></a>设计决策
 由于通信在共享地址空间内更容易，因此您必须选择两种设计方法：在调试会话和 DE 之间设置通信。 或者，在 DE 和程序之间设置通信。 选择以下各项：

- 如果在调试会话和 DE 之间设置通信更有意义，则调试会话会创建 DE，并请求取消附加到程序。 此设计使调试会话并将其放在一个地址空间中，并将运行时环境和程序组合在一起。

- 如果在 DE 和程序之间设置通信更有意义，则运行时环境会共同创建 DE。 这种设计使 SDM 保留在一个地址空间中，并在另一个地址空间中运行。 这种设计通常是使用解释器实现的一种 DE，用来运行脚本语言。

    > [!NOTE]
    > DE 附加到该程序的方式依赖于实现。 DE 与程序之间的通信也依赖于实现。

## <a name="implementation"></a>实现
 以编程方式，当会话调试管理器 (SDM) 首先收到表示要启动的程序的 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) 对象时，它将调用 [Attach](../../extensibility/debugger/reference/idebugprogram2-attach.md) 方法，并向其传递一个 [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) 对象，该对象稍后用于将调试事件传递回 SDM。 然后，该 `IDebugProgram2::Attach` 方法调用 [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) 方法。 有关 SDM 如何接收接口的详细信息 `IDebugProgram2` ，请参阅 [通知端口](../../extensibility/debugger/notifying-the-port.md)。

 如果您的 DE 需要在与要调试的程序相同的地址空间中运行：因为 DE 通常是运行脚本的解释器的一部分，所以该 `IDebugProgramNodeAttach2::OnAttach` 方法返回 `S_FALSE` 。 `S_FALSE`返回指示它已完成附加过程。

 但是，如果在 SDM 的地址空间中运行的 DE 为，则该 `IDebugProgramNodeAttach2::OnAttach` 方法返回 `S_OK` ，或 [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md) 接口根本不是在与要调试的程序关联的 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) 对象上实现的。 在这种情况下，将最终调用 [attach](../../extensibility/debugger/reference/idebugengine2-attach.md) 方法来完成附加操作。

 在后一种情况下，您必须[GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)对 `IDebugProgram2` 传递给方法的对象调用 GetProgramId 方法 `IDebugEngine2::Attach` ，将存储 `GUID` 在本地程序对象中，并在 `GUID` `IDebugProgram2::GetProgramId` 随后对此对象调用方法时返回此方法。 `GUID`用于跨各种调试组件唯一标识程序。

 在方法返回的情况下 `IDebugProgramNodeAttach2::OnAttach` `S_FALSE` ，要用于该程序的将 `GUID` 传递到该方法，并且它是在 `IDebugProgramNodeAttach2::OnAttach` `GUID` 本地程序对象上设置的方法。

 现在已将 DE 附加到节目，并已准备好发送任何启动事件。

## <a name="see-also"></a>另请参阅
- [直接附加到程序](../../extensibility/debugger/attaching-directly-to-a-program.md)
- [通知端口](../../extensibility/debugger/notifying-the-port.md)
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
- [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [附加](../../extensibility/debugger/reference/idebugprogram2-attach.md)
- [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [附加](../../extensibility/debugger/reference/idebugengine2-attach.md)
