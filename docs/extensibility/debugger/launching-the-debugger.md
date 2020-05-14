---
title: 启动调试器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], launching the debugger
- debugger [Debugging SDK], launching
ms.assetid: f24da1a1-f923-48b4-989f-18a22b581d1b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ceb2f484449d1b3f8474a6586d298b057875b342
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738457"
---
# <a name="launch-the-debugger"></a>启动调试器
启动调试器需要发送正确的方法和事件序列及其正确的属性。

## <a name="sequences-of-methods-and-events"></a>方法和事件的顺序

1. 通过选择**调试**菜单，然后选择 **"开始"** 来调用会话调试管理器 （SDM）。 有关详细信息，请参阅[启动程序](../../extensibility/debugger/launching-a-program.md)。

2. SDM 调用[OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)方法。

3. 基于调试引擎 （DE） 过程模型，`IDebugProgramNodeAttach2::OnAttach`该方法返回以下方法之一，确定接下来会发生什么。

     如果`S_FALSE`返回，调试引擎 （DE） 将在虚拟机过程中加载。

     \- 或 -

     如果`S_OK`返回，DE 将在 SDM 的进程中加载。 然后，SDM 执行以下任务：

    1. 致电[GetEngineInfo](../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)获取 DE 的引擎信息。

    2. 共同创建 DE。

    3. 呼叫[附加](../../extensibility/debugger/reference/idebugengine2-attach.md)。

4. DE 将[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)发送到具有`EVENT_SYNC`属性的 SDM。

5. DE 将[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)发送到具有`EVENT_SYNC`属性的 SDM。

6. DE 将[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)发送到具有`EVENT_SYNC`属性的 SDM。

7. DE 将[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)发送到具有`EVENT_SYNC`属性的 SDM。

8. DE 将[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)发送到具有`EVENT_SYNC`属性的 SDM。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
- [启动程序](../../extensibility/debugger/launching-a-program.md)
