---
title: 启动后发送启动事件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], startup events
ms.assetid: 306ea0b4-6d9e-4871-8d8d-a4032d422940
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c71db002420a2b822bffd34f2ae05e712f6a4bb9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713015"
---
# <a name="send-startup-events-after-a-launch"></a>启动后发送启动事件
一旦调试引擎 （DE） 连接到程序，它将一系列启动事件发送回调试会话。

 发回调试会话的启动事件包括：

- 引擎创建事件。

- 程序创建事件。

- 线程创建和模块加载事件。

- 加载完成事件，在加载代码并准备运行时发送，但在执行任何代码之前。

  > [!NOTE]
  > 继续此事件时，将初始化全局变量并运行启动例程。

- 可能的其他线程创建和模块加载事件。

- 入口点事件，表示程序已到达其主要入口点，如**Main**或`WinMain`。 如果 DE 附加到已运行的程序，则通常不会发送此事件。

  在编程上，DE 首先发送会话调试管理器 （SDM） [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)接口，该接口表示引擎创建事件，然后是[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)，它表示程序创建事件。

  这些事件之后通常跟一个或多个[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)线程创建事件和[IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md)模块加载事件。

  加载代码并准备运行时，但在执行任何代码之前，DE 会向 SDM 发送[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)加载完成事件。 最后，如果程序尚未运行，DE 将发送[IDebugEntryPoint2](../../extensibility/debugger/reference/idebugentrypointevent2.md)入口点事件，表示程序已到达其主要入口点并准备好进行调试。

## <a name="see-also"></a>请参阅
- [执行控制](../../extensibility/debugger/control-of-execution.md)
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
