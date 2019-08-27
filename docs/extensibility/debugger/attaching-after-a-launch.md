---
title: 启动后附加 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 5a3600a1-dc20-4e55-b2a4-809736a6ae65
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d7a1ff749d340110707296c9d4958d13a3faa952
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350922"
---
# <a name="attach-after-a-launch"></a>启动后附加
程序启动后，调试会话已准备好附加到上述程序的调试引擎 (DE)。

## <a name="design-decisions"></a>设计决策
 因为通信更容易共享的地址空间内，必须选择两种设计方法是： 设置调试会话和设备之间的通信。 或者，设置 DE 和程序之间的通信。 在以下选择：

- 如果它更有意义设置调试会话和设备之间的通信，调试会话共同创建 DE 并询问 DE 将附加到该程序。 这种设计使调试会话，DE 一起中一个地址空间的运行时环境和程序中另一个合并在一起。

- 如果它更有意义设置 DE 与程序之间的通信，运行时环境共同创建 DE。 这种设计离开一个地址空间和 DE、 运行时环境和程序中的 SDM 中另一个合并在一起。 这种设计是典型的部署使用解释器以运行脚本化的语言实现。

    > [!NOTE]
    > 如何将 DE 附加到该程序是依赖于实现的。 DE 和程序之间的通信也是依赖于实现的。

## <a name="implementation"></a>实现
 以编程方式，当会话调试管理器 (SDM) 首次收到[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)对象，该对象表示要启动的程序，它将调用[附加](../../extensibility/debugger/reference/idebugprogram2-attach.md)方法，并向其传递[IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)对象，它是更高版本用于传递回 SDM 调试事件。 `IDebugProgram2::Attach`方法随后调用[OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)方法。 有关详细信息如何 SDM 接收`IDebugProgram2`接口，请参阅[通知端口](../../extensibility/debugger/notifying-the-port.md)。

 如果你 DE 需要运行的程序所在的同一个地址空间中进行调试： 因为 DE 通常是正在运行一个脚本的解释器的一部分`IDebugProgramNodeAttach2::OnAttach`方法将返回`S_FALSE`。 `S_FALSE`返回指示它已附加过程完成。

 如果，但是，DE 运行 SDM 的地址空间中：`IDebugProgramNodeAttach2::OnAttach`方法将返回`S_OK`，或[IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)上根本不实现接口[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)与正在调试的程序关联的对象。 在这种情况下，[附加](../../extensibility/debugger/reference/idebugengine2-attach.md)方法最终调用以完成附加操作。

 在后一种情况下，必须调用[GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)方法`IDebugProgram2`对象传递给`IDebugEngine2::Attach`方法、 应用商店`GUID`本地程序中对象，并返回此`GUID`时`IDebugProgram2::GetProgramId`随后对此对象调用方法。 `GUID`用于在各种调试组件之间唯一地标识该程序。

 情况下`IDebugProgramNodeAttach2::OnAttach`方法返回`S_FALSE`，则`GUID`要用于该程序将传递给该方法，并且`IDebugProgramNodeAttach2::OnAttach`方法以设置`GUID`上的本地程序对象。

 DE 现在已附加到程序中并准备好发送任何启动事件。

## <a name="see-also"></a>请参阅
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