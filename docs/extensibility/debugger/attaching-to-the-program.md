---
title: 将附加到程序 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 9a3f5b83-60b5-4ef0-91fe-a432105bd066
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d1cc66dbade730409406a7dc3f3208c4d5147fa6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66332636"
---
# <a name="attach-to-the-program"></a>附加到程序
与相应的端口注册您的程序后，必须将调试器附加到你想要调试的程序。

## <a name="choose-how-to-attach"></a>选择要附加的方式
 有三种方法会话调试管理器 (SDM) 尝试将附加到正在调试的程序。

1. 程序的调试引擎通过启动[LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)方法 （典型的解释型语言，例如） SDM 来获取[IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)从接口[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)与附加到的程序关联的对象。 如果可以获取 SDM`IDebugProgramNodeAttach2`接口，然后调用 SDM [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)方法。 `IDebugProgramNodeAttach2::OnAttach`方法将返回`S_OK`指示它未附加到该程序，并可以进行其他尝试将附加到该程序。

2. 如果可以获取 SDM [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md)附加到 SDM 调用该程序从接口[附加](../../extensibility/debugger/reference/idebugprogramex2-attach.md)方法。 这种方法是典型的未通过端口提供程序远程启动的程序。

3. 如果程序不能通过附加`IDebugProgramNodeAttach2::OnAttach`或`IDebugProgramEx2::Attach`方法，SDM 加载 （如果尚未加载） 的调试引擎通过调用`CoCreateInstance`函数，然后调用[附加](../../extensibility/debugger/reference/idebugengine2-attach.md)方法。 这种方法是典型的本地启动端口提供程序的程序。

    还有可能用于自定义端口提供程序来调用`IDebugEngine2::Attach`中的自定义端口供应商的实现方法`IDebugProgramEx2::Attach`方法。 通常在这种情况下，自定义端口提供程序将启动远程计算机上的调试引擎。

   会话调试管理器 (SDM) 调用时，才能够达到附件[附加](../../extensibility/debugger/reference/idebugengine2-attach.md)方法。

   如果要调试的应用程序在同一进程中运行你 DE，则必须实现的以下方法[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md):

- [GetHostName](../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)

- [GetHostPid](../../extensibility/debugger/reference/idebugprogramnode2-gethostpid.md)

- [GetProgramName](../../extensibility/debugger/reference/idebugprogramnode2-getprogramname.md)

  之后`IDebugEngine2::Attach`方法调用时，请执行以下步骤的实现中`IDebugEngine2::Attach`方法：

1. 发送[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)到 SDM 事件对象。 有关详细信息，请参阅[将事件发送](../../extensibility/debugger/sending-events.md)。

2. 调用[GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)方法[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)对象传递给`IDebugEngine2::Attach`方法。

     这将返回`GUID`用于标识程序。 `GUID`必须存储在该对象表示本地编程为 DE，且必须返回何时`IDebugProgram2::GetProgramId`上调用方法`IDebugProgram2`接口。

    > [!NOTE]
    > 如果你实现了`IDebugProgramNodeAttach2`接口，该程序的`GUID`传递给`IDebugProgramNodeAttach2::OnAttach`方法。 这`GUID`用于控制程序`GUID`返回的`IDebugProgram2::GetProgramId`方法。

3. 发送[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件对象，以通知 SDM 的本地`IDebugProgram2`创建对象时用于表示 DE 程序。 有关详细信息，请参阅[发送事件](../../extensibility/debugger/sending-events.md)。

    > [!NOTE]
    > 这是不相同`IDebugProgram2`对象传递到`IDebugEngine2::Attach`方法。 以前已通过`IDebugProgram2`对象被端口仅识别，是一个单独的对象。

## <a name="see-also"></a>请参阅
- [基于启动的附件](../../extensibility/debugger/launch-based-attachment.md)
- [发送事件](../../extensibility/debugger/sending-events.md)
- [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)
- [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md)
- [附加](../../extensibility/debugger/reference/idebugprogramex2-attach.md)
- [附加](../../extensibility/debugger/reference/idebugengine2-attach.md)
