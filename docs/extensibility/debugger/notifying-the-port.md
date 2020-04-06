---
title: 通知端口 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ports, notification
ms.assetid: f9fce48e-7d4e-4627-a0fb-77b75428146a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ff94c20969e77bcc70af2f5a16137e09366a0d7d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738324"
---
# <a name="notify-the-port"></a>通知端口
启动程序后，必须通知端口，如下所示：

1. 当端口收到新的程序节点时，它将程序创建事件发送回调试会话。 该事件带有一个表示程序的接口。

2. 调试会话查询可以附加到的调试引擎 （DE） 标识符的程序。

3. 调试会话检查 DE 是否位于该程序的允许 D 列表中。 调试会话从解决方案的活动程序设置获取此列表，该设置最初由调试包传递给它。

    DE 必须位于允许列表中，否则 DE 将不会附加到程序。

   在编程上，当端口首次收到新的程序节点时，它会创建一个[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)接口来表示程序。

> [!NOTE]
> 这不应与调试引擎 （DE） 以后创建的`IDebugProgram2`接口混淆。

 端口通过 COM`IConnectionPoint`接口将[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)程序创建事件发送回会话调试管理器 （SDM）。

> [!NOTE]
> 这不应与`IDebugProgramCreateEvent2`DE 稍后发送的接口混淆。

 除了事件接口本身外，端口还发送[IDebugPort2、IDebugProcess2](../../extensibility/debugger/reference/idebugport2.md)和[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)接口，分别表示端口、进程和程序。 [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md) SDM 调用[IDebugProgram2：：获取引擎信息](../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)以获取可以调试程序的 DE GUID。 GUID 最初从[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)接口获得。

 SDM 检查 DE 是否位于允许的 DE 列表中。 SDM 从解决方案的活动程序设置获取此列表，该设置最初由调试包传递给它。 DE 必须位于允许的列表中，否则不会附加到程序。

 一旦 DE 的标识已知，SDM 就可以将其附加到程序。

## <a name="see-also"></a>请参阅
- [启动程序](../../extensibility/debugger/launching-a-program.md)
- [启动后附加](../../extensibility/debugger/attaching-after-a-launch.md)
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
