---
title: 附加到程序 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 9a3f5b83-60b5-4ef0-91fe-a432105bd066
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8f39b489a57ab93ba5f2d116738c591bd53ff95f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739250"
---
# <a name="attach-to-the-program"></a>附加到程序
在适当的端口注册程序后，必须将调试器附加到要调试的程序。

## <a name="choose-how-to-attach"></a>选择如何附加
 会话调试管理器 （SDM） 尝试附加到正在调试的程序有三种方式。

1. 对于调试引擎通过[Launch暂停](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)方法启动的程序（例如，典型的解释语言），SDM 从与所附加到的程序关联的[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)对象获取[IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)接口。 如果 SDM 可以获取`IDebugProgramNodeAttach2`接口，则 SDM 然后调用[OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)方法。 该方法`IDebugProgramNodeAttach2::OnAttach`返回`S_OK`以指示它未附加到程序，并且可以尝试附加到该程序。

2. 如果 SDM 可以从所附加到的程序获取[IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md)接口，则 SDM 将调用[附加](../../extensibility/debugger/reference/idebugprogramex2-attach.md)方法。 此方法对于端口供应商远程启动的程序是典型的。

3. 如果无法`IDebugProgramNodeAttach2::OnAttach`通过 或 方法`IDebugProgramEx2::Attach`附加程序，则 SDM 通过调用`CoCreateInstance`函数加载调试引擎（如果尚未加载），然后调用[Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)方法。 此方法对于端口供应商在本地启动的程序是典型的。

    自定义端口供应商也可以调用`IDebugEngine2::Attach`自定义端口供应商实现该方法`IDebugProgramEx2::Attach`的方法。 在这种情况下，自定义端口供应商在远程计算机上启动调试引擎。

   当会话调试管理器 （SDM） 调用附加方法时，实现[连接](../../extensibility/debugger/reference/idebugengine2-attach.md)。

   如果 DE 与要调试的应用程序在同一进程中运行，则必须实现[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)的以下方法：

- [GetHostName](../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)

- [GetHostPid](../../extensibility/debugger/reference/idebugprogramnode2-gethostpid.md)

- [GetProgramName](../../extensibility/debugger/reference/idebugprogramnode2-getprogramname.md)

  调用方法`IDebugEngine2::Attach`后，在`IDebugEngine2::Attach`方法的实现中按照以下步骤操作：

1. 将[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)事件对象发送到 SDM。 有关详细信息，请参阅[发送事件](../../extensibility/debugger/sending-events.md)。

2. 在传递给`IDebugEngine2::Attach`该方法的[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)对象上调用[GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)方法。

     这将返回用于`GUID`标识程序的 。 `GUID`必须存储在表示 DE 的本地程序的对象中，并且必须在`IDebugProgram2`接口上调用`IDebugProgram2::GetProgramId`方法时返回它。

    > [!NOTE]
    > 如果实现接口，`IDebugProgramNodeAttach2`程序将`GUID`传递给 方法`IDebugProgramNodeAttach2::OnAttach`。 这`GUID`用于`GUID``IDebugProgram2::GetProgramId`方法返回的程序。

3. 发送[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件对象，通知 SDM 本地`IDebugProgram2`对象已创建以向 DE 表示程序。 有关详细信息，请参阅[发送事件](../../extensibility/debugger/sending-events.md)。

    > [!NOTE]
    > 这不是传递到`IDebugProgram2``IDebugEngine2::Attach`方法的相同对象。 以前传递`IDebugProgram2`的对象仅由端口识别，并且是一个单独的对象。

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
- [Attach](../../extensibility/debugger/reference/idebugprogramex2-attach.md)
- [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)
