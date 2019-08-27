---
title: 启动调试器 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], launching the debugger
- debugger [Debugging SDK], launching
ms.assetid: f24da1a1-f923-48b4-989f-18a22b581d1b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 99b8dcd9647cf9a55bd5cc29d082c8d79e57f302
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353853"
---
# <a name="launch-the-debugger"></a>启动调试器
启动调试器需要发送正确的方法和具有适当的属性的事件顺序。

## <a name="sequences-of-methods-and-events"></a>方法和事件的序列

1. 会话调试管理器 (SDM) 调用通过选择**调试**菜单，，然后选择**启动**。 有关详细信息，请参阅[启动某个程序](../../extensibility/debugger/launching-a-program.md)。

2. SDM 调用[OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)方法。

3. 基于调试引擎 (DE) 进程模型，`IDebugProgramNodeAttach2::OnAttach`方法返回确定接下来会发生的以下方法之一。

     如果`S_FALSE`返回时，调试引擎 (DE) 是要加载正在虚拟机。

     或

     如果`S_OK`返回，DE 是要加载 SDM 的过程中。 SDM 然后执行以下任务：

    1. 调用[GetEngineInfo](../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)了解 DE 引擎。

    2. 共同创建 DE。

    3. 调用[附加](../../extensibility/debugger/reference/idebugengine2-attach.md)。

4. DE 发送[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)到使用 SDM`EVENT_SYNC`属性。

5. DE 发送[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)到使用 SDM`EVENT_SYNC`属性。

6. DE 发送[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)到使用 SDM`EVENT_SYNC`属性。

7. DE 发送[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)到使用 SDM`EVENT_SYNC`属性。

8. DE 发送[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)到使用 SDM`EVENT_SYNC`属性。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
- [启动程序](../../extensibility/debugger/launching-a-program.md)