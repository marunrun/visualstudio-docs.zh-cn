---
title: 通知端口 |Microsoft Docs
description: 了解启动程序后如何通知端口。 本文包含详细说明。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: e9a838879e7c1eb590bb16cd12a6bf345de8031a
ms.sourcegitcommit: 42981ace63c0f2b087de5703ca76b8dcdd93a719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2020
ms.locfileid: "96606614"
---
# <a name="notify-the-port"></a>通知端口
启动程序后，必须通知端口，如下所示：

1. 当某个端口接收到新的程序节点时，它会将一个程序创建事件发回到调试会话。 该事件携带表示程序的接口。

2. 调试会话在程序中查询可附加到的 (DE) 的调试引擎标识符。

3. 调试会话会检查是否已在该程序的允许 DEs 列表中找到 DE。 调试会话从解决方案的活动程序设置获取此列表，此列表最初由调试包传递给它。

    DE 必须位于允许列表上，否则不会将此 de 附加到程序。

   以编程方式，当某个端口首次接收新的程序节点时，它将创建一个 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) 接口以表示程序。

> [!NOTE]
> 这不应与 `IDebugProgram2` 稍后由调试引擎创建的接口混淆 (DE) 。

 端口通过 COM 接口将 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) 程序创建事件返回到会话调试管理器 (SDM) `IConnectionPoint` 。

> [!NOTE]
> 这不应与 `IDebugProgramCreateEvent2` 接口混淆，后者稍后会通过取消。

 该端口与事件接口本身一起发送 [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)、 [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)和 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) 接口，分别表示端口、进程和程序。 SDM 调用 [IDebugProgram2：： GetEngineInfo](../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md) 以获取可调试程序的 DE 的 GUID。 GUID 最初是从 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) 接口获取的。

 SDM 检查是否在允许的 DEs 列表上进行了 DE。 SDM 从解决方案的活动程序设置获取此列表，这些设置最初由调试包传递给它。 DE 必须位于允许列表上，否则将不会附加到程序中。

 一旦知道了 DE 标识，SDM 就可以将其附加到程序。

## <a name="see-also"></a>请参阅
- [启动程序](../../extensibility/debugger/launching-a-program.md)
- [启动后附加](../../extensibility/debugger/attaching-after-a-launch.md)
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
