---
title: 附加到程序 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 9a3f5b83-60b5-4ef0-91fe-a432105bd066
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 00b9780d0d302b9e067feed057d1a8d49c5f9fc0
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903211"
---
# <a name="attach-to-the-program"></a>附加到程序
使用适当的端口注册程序后，必须将调试器附加到要调试的程序。

## <a name="choose-how-to-attach"></a>选择附加方法
 会话调试管理器（SDM）尝试附加到正在调试的程序的方法有三种。

1. 对于由调试引擎通过[LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)方法启动的程序（例如，典型的解释语言），SDM 从与附加到的程序相关联的[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)对象获取[IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)接口。 如果 SDM 可以获取 `IDebugProgramNodeAttach2` 接口，则 sdm 将调用[OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)方法。 `IDebugProgramNodeAttach2::OnAttach`方法返回， `S_OK` 指示它未附加到程序，并且可以进行其他尝试附加到程序。

2. 如果 SDM 可以从附加到的程序获取[IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md)接口，则 sdm 将调用[Attach](../../extensibility/debugger/reference/idebugprogramex2-attach.md)方法。 此方法对于由端口提供程序远程启动的程序是典型的。

3. 如果程序无法通过 `IDebugProgramNodeAttach2::OnAttach` 或 `IDebugProgramEx2::Attach` 方法附加，则 SDM 会通过调用函数加载调试引擎（如果尚未加载）， `CoCreateInstance` 然后调用[Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)方法。 此方法对于端口供应商在本地启动的程序是典型的。

    自定义端口供应商也可以 `IDebugEngine2::Attach` 在方法的自定义端口供应商实现中调用方法 `IDebugProgramEx2::Attach` 。 通常，在这种情况下，自定义端口供应商将在远程计算机上启动调试引擎。

   当会话调试管理器（SDM）调用[Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)方法时，将实现附件。

   如果在与要调试的应用程序相同的进程中运行，则必须实现以下[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)方法：

- [GetHostName](../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)

- [GetHostPid](../../extensibility/debugger/reference/idebugprogramnode2-gethostpid.md)

- [GetProgramName](../../extensibility/debugger/reference/idebugprogramnode2-getprogramname.md)

  `IDebugEngine2::Attach`调用方法后，请在方法的实现中执行以下步骤 `IDebugEngine2::Attach` ：

1. 向 SDM 发送[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)事件对象。 有关详细信息，请参阅[发送事件](../../extensibility/debugger/sending-events.md)。

2. 对传递给该方法的[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)对象调用[GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)方法 `IDebugEngine2::Attach` 。

     这会返回 `GUID` 用于标识程序的。 `GUID`必须存储在表示要取消的本地程序的对象中，当在 `IDebugProgram2::GetProgramId` 接口上调用方法时，必须返回该对象 `IDebugProgram2` 。

    > [!NOTE]
    > 如果实现 `IDebugProgramNodeAttach2` 接口，则会将程序 `GUID` 传递给 `IDebugProgramNodeAttach2::OnAttach` 方法。 这 `GUID` 用于 `GUID` 方法返回的程序 `IDebugProgram2::GetProgramId` 。

3. 发送[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件对象，通知 SDM `IDebugProgram2` 已创建本地对象来表示要取消的程序。 有关详细信息，请参阅[发送事件](../../extensibility/debugger/sending-events.md)。

    > [!NOTE]
    > 这不同于 `IDebugProgram2` 传递到方法中的对象 `IDebugEngine2::Attach` 。 之前传递的 `IDebugProgram2` 对象仅由端口识别，并且是一个单独的对象。

## <a name="see-also"></a>另请参阅
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
