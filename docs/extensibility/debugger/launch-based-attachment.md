---
title: 基于启动的附件 |Microsoft Docs
description: 了解基于启动的程序的附件，该程序是自动的，并遵循与手动附件类似的路径。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, launching
- debug engines, attaching to programs
ms.assetid: 362f00ac-1909-4a3a-bacb-c0ceb5549816
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7e041c692a833b7d0a1891c078388a3f5b2d11e4
ms.sourcegitcommit: 42981ace63c0f2b087de5703ca76b8dcdd93a719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2020
ms.locfileid: "96606666"
---
# <a name="launch-based-attachment"></a>基于启动的附件
程序的基于启动的附件是自动的。 当由 SDM 启动托管程序的进程时，基于启动的附件将遵循与手动附件方法类似的路径。 有关信息，请参阅 [附加到计划](../../extensibility/debugger/attaching-to-the-program.md)。

## <a name="the-attaching-process"></a>附加进程
 主要区别是 **连接** 调用后的事件序列，如下所示：

1. 向 SDM 发送 **IDebugEngineCreateEvent2** 事件对象。 有关详细信息，请参阅 [发送事件](../../extensibility/debugger/sending-events.md)。

2. `IDebugProgram2::GetProgramId`在传递给 **Attach** 方法的 **IDebugProgram2** 接口上调用方法。

3. 发送 **IDebugProgramCreateEvent2** 事件对象，通知 SDM 创建了本地 **IDebugProgram2** 对象，以表示该程序被取消。

4. 发送 [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) 事件对象来通知 SDM，为启动的进程创建新线程。

## <a name="see-also"></a>请参阅
- [发送所需的事件](../../extensibility/debugger/sending-the-required-events.md)
- [启用要调试的程序](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
