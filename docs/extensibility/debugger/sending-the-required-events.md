---
title: 发送所需的事件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], required events
ms.assetid: 08319157-43fb-44a9-9a63-50b919fe1377
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 44ef1bb6c436faaefb309ab62db02ee43a0486ab
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66345598"
---
# <a name="send-the-required-events"></a>发送所需的事件
使用此过程来发送所需的事件。

## <a name="process-for-sending-required-events"></a>用于发送所需的事件的过程
 以下事件是必需的此顺序时创建调试引擎 (DE) 并将其附加到程序中：

1. 发送[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)会话调试管理器 (SDM) DE 初始化用于调试的进程中的一个或多个程序时的事件对象。

2. 要调试程序附加到，当发送[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)到 SDM 事件对象。 此事件可能 stopping 事件，具体取决于您引擎的设计。

3. 如果程序附加到进程启动时，发送[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)到 SDM 通知新线程的 IDE 的事件对象。 此事件可能 stopping 事件，具体取决于您引擎的设计。

4. 发送[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)到 SDM 正在调试的程序时完成的加载或将附加到程序完成的事件对象。 此事件必须停止事件。

5. 如果启动要调试的应用程序时，发送[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)到 SDM 代码运行时体系结构中的第一个指令时要执行的事件对象。 此事件始终是停止事件。 当单步执行调试会话，IDE 将停止对此事件。

> [!NOTE]
> 许多语言使用全局初始值设定项或外部、 预编译函数 （从的 CRT 库或 _Main） 在其代码的开头。 如果你正在调试的程序的语言包含下列任意一种元素之前的初始入口点，运行此代码并发送入口点事件时的用户入口点，如**主要**或`WinMain`，是已达到。

## <a name="see-also"></a>请参阅
- [启用要进行调试的程序](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)