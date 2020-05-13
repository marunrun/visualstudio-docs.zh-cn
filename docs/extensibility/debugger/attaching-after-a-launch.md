---
title: 启动后附加 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739281"
---
# <a name="attach-after-a-launch"></a>启动后附加
程序启动后，调试会话已准备好将调试引擎 （DE） 附加到上述程序。

## <a name="design-decisions"></a>设计决策
 由于在共享地址空间内通信更容易，因此必须在两种设计方法之间进行选择：在调试会话和 DE 之间设置通信。 或者，设置 DE 和程序之间的通信。 在以下两者之间选择：

- 如果设置调试会话和 DE 之间的通信更有意义，则调试会话将共同创建 DE，并要求 DE 附加到程序。 此设计将调试会话和 DE 放在一个地址空间中，并将运行时环境和程序放在另一个地址空间中。

- 如果设置 DE 和程序之间的通信更有意义，则运行时环境将共同创建 DE。 此设计将 SDM 保留在一个地址空间和 DE、运行时环境和程序一起放在另一个地址空间中。 此设计是典型的 DE，该 DE 使用解释器实现以运行脚本语言。

    > [!NOTE]
    > DE 如何附加到程序取决于实现。 DE 和程序之间的通信也依赖于实现。

## <a name="implementation"></a>实现
 在编程上，当会话调试管理器 （SDM） 首次收到表示要启动的程序的[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)对象时，它将调用[Attach](../../extensibility/debugger/reference/idebugprogram2-attach.md)方法，将其传递为[IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)对象，该对象后来用于将调试事件传回 SDM。 然后`IDebugProgram2::Attach`，该方法调用[OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)方法。 有关 SDM 如何接收`IDebugProgram2`接口的详细信息，请参阅[通知端口](../../extensibility/debugger/notifying-the-port.md)。

 如果 DE 需要在与正在调试的程序相同的地址空间中运行：因为 DE 通常是运行脚本的解释器的一部分，`IDebugProgramNodeAttach2::OnAttach`因此该方法将返回`S_FALSE`。 `S_FALSE`返回表示已完成附加过程。

 但是，如果 DE 在 SDM 的地址空间`IDebugProgramNodeAttach2::OnAttach`中运行：该方法返回`S_OK`，或者[IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)接口根本不在与要调试的程序关联的[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)对象上实现。 在这种情况下，最终调用[Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)方法以完成附加操作。

 在后一种情况下，必须在传递给`IDebugProgram2``IDebugEngine2::Attach`该方法的对象上调用`GUID`[GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)方法，将 存储在本地程序对象中，并在随后调用`IDebugProgram2::GetProgramId`此对象的方法时返回`GUID`此方法。 `GUID`用于在各种调试组件中唯一地标识程序。

 `IDebugProgramNodeAttach2::OnAttach`在返回的方法中`S_FALSE`，用于程序的`GUID`将传递给该方法，`IDebugProgramNodeAttach2::OnAttach`它是在本地程序对象`GUID`上设置 的方法。

 DE 现在附加到该程序，并准备发送任何启动事件。

## <a name="see-also"></a>请参阅
- [直接附加到程序](../../extensibility/debugger/attaching-directly-to-a-program.md)
- [通知端口](../../extensibility/debugger/notifying-the-port.md)
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
- [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [Attach](../../extensibility/debugger/reference/idebugprogram2-attach.md)
- [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)
