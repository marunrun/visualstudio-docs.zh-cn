---
title: 发送所需事件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], required events
ms.assetid: 08319157-43fb-44a9-9a63-50b919fe1377
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cc83b47e53607fe1111ececbbf892c96f7bbb639
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712998"
---
# <a name="send-the-required-events"></a>发送所需事件
使用此过程发送所需事件。

## <a name="process-for-sending-required-events"></a>发送所需事件的过程
 按照此顺序，创建调试引擎 （DE） 并将其附加到程序时，需要以下事件：

1. 当 DE 初始化以调试进程中的一个或多个程序时，将[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)事件对象发送到会话调试管理器 （SDM）。

2. 将要调试的程序附加到时，将[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件对象发送到 SDM。 此事件可能是停止事件，具体取决于您的发动机设计。

3. 如果程序在启动进程时附加到，则向 SDM 发送[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)事件对象以通知新线程的 IDE。 此事件可能是停止事件，具体取决于您的发动机设计。

4. 当正在调试的程序完成加载或附加到程序时，将[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)事件对象发送到 SDM。 此事件必须是停止事件。

5. 如果启动要调试的应用程序，则在运行时体系结构中的第一个代码指令即将执行时，向 SDM 发送[IDebugEntryPoint2](../../extensibility/debugger/reference/idebugentrypointevent2.md)事件对象。 此事件始终是停止事件。 踏入调试会话时，IDE 将在此事件中停止。

> [!NOTE]
> 许多语言在其代码的开头使用全局初始化程序或外部预编译函数（来自 CRT 库或_Main）。 如果要调试的程序的语言在初始入口点之前包含这些类型的元素之一，则运行此代码，并在达到用户入口点（如**主**或`WinMain`）时发送入口点事件。

## <a name="see-also"></a>请参阅
- [启用对程序进行调试](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
