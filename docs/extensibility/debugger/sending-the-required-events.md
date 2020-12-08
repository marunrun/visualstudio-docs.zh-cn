---
title: 正在发送所需的事件 |Microsoft Docs
description: 了解创建调试引擎并将其附加到 Visual Studio 调试中的程序时所需的有序事件。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 49c85e3d371bfd729d55e9d17a6c8de61924e35f
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2020
ms.locfileid: "96845305"
---
# <a name="send-the-required-events"></a>发送所需的事件
使用此过程来发送所需的事件。

## <a name="process-for-sending-required-events"></a>发送所需事件的过程
 以下事件是必需的，在创建调试引擎时 (取消) 并将其附加到程序：

1. 为调试进程中的一个或多个程序而初始化 DE 后，将 [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) 事件对象发送到会话调试管理器 (SDM) 。

2. 当要调试的程序附加到时，将 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) 事件对象发送到 SDM。 此事件可能是一个停止事件，具体取决于您的引擎设计。

3. 如果在进程启动时将程序附加到，请将 [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) 事件对象发送到 SDM，以通知 IDE 新线程。 此事件可能是一个停止事件，具体取决于您的引擎设计。

4. 当正在调试的程序完成加载或附加到程序完成时，将 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) 事件对象发送到 SDM。 此事件必须是停止事件。

5. 如果要调试的应用程序已启动，则在运行时结构中的第一个代码指令将要执行时，将 [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) 事件对象发送到 SDM。 此事件始终是停止事件。 单步执行调试会话时，IDE 将在此事件停止。

> [!NOTE]
> 许多语言使用 (从 CRT 库中的全局初始值设定项或外部预编译函数，或 _Main) 在其代码的开头。 如果正在调试的程序的语言在初始入口点之前包含这两种类型的元素，则会运行此代码，并在达到用户入口点（如 **main** 或）时发送入口点事件 `WinMain` 。

## <a name="see-also"></a>请参阅
- [启用要调试的程序](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
