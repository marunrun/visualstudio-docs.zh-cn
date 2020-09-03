---
title: 启动调试器 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738457"
---
# <a name="launch-the-debugger"></a>启动调试器
启动调试器要求发送正确的方法和事件顺序及其正确的特性。

## <a name="sequences-of-methods-and-events"></a>方法和事件的序列

1. 通过选择 " **调试** " 菜单，然后选择 " **启动**"，可调用会话调试管理器 (SDM) 。 有关详细信息，请参阅 [启动程序](../../extensibility/debugger/launching-a-program.md)。

2. SDM 调用 [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) 方法。

3. 根据调试引擎 (DE) 进程模型，该方法将 `IDebugProgramNodeAttach2::OnAttach` 返回以下方法之一，该方法决定接下来会发生的情况。

     如果 `S_FALSE` 返回，将在虚拟机的进程中加载 (DE) 调试引擎。

     - 或 -

     如果 `S_OK` 返回，则将在 SDM 的进程中加载 DE。 然后，SDM 会执行以下任务：

    1. 调用 [GetEngineInfo](../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md) 以获取 DE 的引擎信息。

    2. 共同创建 DE。

    3. 调用 [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)。

4. DE 使用特性向 SDM 发送 [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) `EVENT_SYNC` 。

5. DE 使用特性向 SDM 发送 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) `EVENT_SYNC` 。

6. DE 使用特性向 SDM 发送 [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) `EVENT_SYNC` 。

7. DE 使用特性向 SDM 发送 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) `EVENT_SYNC` 。

8. DE 使用特性向 SDM 发送 [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) `EVENT_SYNC` 。

## <a name="see-also"></a>另请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
- [启动程序](../../extensibility/debugger/launching-a-program.md)
