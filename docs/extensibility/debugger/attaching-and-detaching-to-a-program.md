---
title: 附加和分离到程序 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
- debug engines, detaching from programs
ms.assetid: 79dcbb9b-c7f8-40fc-8a00-f37fe1934f51
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d8bd6ea4b51c56a3cc42036b7bd26d34ff3a3eff
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739265"
---
# <a name="attaching-and-detaching-to-a-program"></a>附加和分离到程序
附加调试器需要发送具有正确属性的正确方法和事件序列。

## <a name="sequence-of-methods-and-events"></a>方法和事件的顺序

1. 会话调试管理器 （SDM） 调用[OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)方法。

    基于调试引擎 （DE） 过程模型，`IDebugProgramNodeAttach2::OnAttach`该方法返回以下方法之一，确定接下来会发生什么。

    如果`S_FALSE`返回，调试引擎已成功连接到该程序。 否则，将调用[附加](../../extensibility/debugger/reference/idebugengine2-attach.md)方法以完成附加过程。

    如果`S_OK`返回，DE 将加载到与 SDM 相同的进程中。 SDM 执行以下任务：

   1. 致电[GetEngineInfo](../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)获取 DE 的引擎信息。

   2. 共同创建 DE。

   3. 呼叫[附加](../../extensibility/debugger/reference/idebugengine2-attach.md)。

2. DE 将[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)发送到具有`EVENT_SYNC`属性的 SDM。

3. DE 将[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)发送到具有`EVENT_SYNC`属性的 SDM。

4. DE 将[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)发送到具有`EVENT_SYNC_STOP`属性的 SDM。

   从程序分离是一个简单的两步过程，如下所示：

5. SDM 调用[分离](../../extensibility/debugger/reference/idebugprogram2-detach.md)。

6. DE 发送[IDebugProgram破坏事件2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
