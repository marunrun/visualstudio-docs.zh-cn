---
title: 基于启动的附件 |微软文档
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
ms.openlocfilehash: 4910a97350366500b56593ec0076fdf0990b6d8f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738470"
---
# <a name="launch-based-attachment"></a>基于启动的附件
基于启动的程序附件是自动的。 当托管程序的进程由 SDM 启动时，基于启动的附件遵循类似于手动附件方法的路径。 有关详细信息，请参阅[附加到程序](../../extensibility/debugger/attaching-to-the-program.md)。

## <a name="the-attaching-process"></a>附加过程
 主要区别是**附加**调用后的事件序列，如下所示：

1. 将**IDebugEngineCreateEvent2**事件对象发送到 SDM。 有关详细信息，请参阅[发送事件](../../extensibility/debugger/sending-events.md)。

2. 调用传递给`IDebugProgram2::GetProgramId`**附加**方法的**IDebugProgram2**接口上的方法。

3. 发送**IDebugProgramCreateEvent2**事件对象，通知 SDM 本地**IDebugProgram2**对象是为了向 DE 表示程序。

4. 发送[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)事件对象，通知 SDM 为启动的进程创建新线程。

## <a name="see-also"></a>请参阅
- [发送所需事件](../../extensibility/debugger/sending-the-required-events.md)
- [启用对程序进行调试](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
