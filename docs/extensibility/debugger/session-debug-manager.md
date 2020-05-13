---
title: 会话调试管理器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- session debug manager, unifying session views
- session debug manager, broadcasting
- debugging [Debugging SDK], session debug manager
- session debug manager
- session debug manager, debug engine multiplexing
- session debug manager, delegating
ms.assetid: fbb1928d-dddc-43d1-98a4-e23b0ecbae09
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 953b4e948ef5e21531a3e73bceed3a363ed3cec5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712884"
---
# <a name="session-debug-manager"></a>会话调试管理器
会话调试管理器 （SDM） 管理任意数量的调试引擎 （DE），这些引擎正在任意数量的跨任意数量的计算机在多个进程中调试任意数量的程序。 除了作为调试引擎多路复用器外，SDM 还为 IDE 提供了调试会话的统一视图。

## <a name="session-debug-manager-operation"></a>会话调试管理器操作
 会话调试管理器 （SDM） 管理 DE。 可以同时在计算机上运行多个调试引擎。 要对 DE 进行多路复用，SDM 会从 DE 包装多个接口，并将它们作为单个接口公开给 IDE。

 为了提高性能，某些接口不会进行多路复用。 相反，它们直接从 DE 使用，并且对这些接口的调用不会通过 SDM。 例如，与内存、代码和文档上下文一起使用的接口不会进行多路复用，因为它们是指特定 DE 调试的特定程序中的特定指令、内存或文档。 没有其他 DE 需要参与该级别的通信。

 并非所有上下文都如此。 对表达式计算上下文接口的调用通过 SDM。 在表达式计算期间，SDM 会包装它给 IDE 的[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)接口，因为计算该表达式时，它可能涉及多个正在调试程序的 IDE，这些进程可能在同一线程上运行。

 SDM 通常充当委派机制，但它可以充当广播机制。 例如，在表达式计算期间，SDM 充当广播机制，通知所有 D 可以运行指定线程上的代码。 同样，当 SDM 收到停止事件时，它将广播到它们应停止运行的节目。 调用步骤时，SDM 会广播到它们可以继续运行的程序。 断点也会广播到每个 DE。

 SDM 不跟踪当前程序、线程或堆栈帧。 进程、程序和线程信息与特定调试事件一起发送到 SDM。

## <a name="see-also"></a>请参阅
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [调试器组件](../../extensibility/debugger/debugger-components.md)
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)
