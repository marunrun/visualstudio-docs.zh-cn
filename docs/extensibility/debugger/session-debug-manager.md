---
title: 会话调试管理器 |Microsoft Docs
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
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6c7dd40796fbf0141cc60bf86204bce462594f8f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348563"
---
# <a name="session-debug-manager"></a>会话调试管理器
会话调试管理器 (SDM) 管理任意数量的任意数量的多个进程中的程序调试跨任意数量的计算机的调试引擎 (DE)。 除了多路复用器的调试引擎外，SDM 提供到 IDE 的调试会话的统一的视图。

## <a name="session-debug-manager-operation"></a>会话调试管理器操作
 会话调试管理器 (SDM) 管理 DE。 可以在同一时间运行的计算机上的多个调试引擎。 若要进行多路复用 DEs，SDM 包装数个 DEs 的接口，并将其公开到单个接口作为 IDE。

 若要提高性能，某些接口不是多路复用。 相反，它们用于直接从 DE，，SDM，不会对这些接口的调用。 例如，与内存、 代码和文档上下文一起使用的接口不是多路复用，因为它们引用的特定指令、 内存或在特定程序通过特定 DE 调试中的文档。 要在该级别的通信中涉及任何其他 DE 不要求。

 这不是所有上下文的则返回 true。 对表达式求值上下文接口的调用会经历 SDM。 在表达式计算期间 SDM 包装[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)的界面，它使 IDE 因为当计算该表达式时，它可能涉及多个正在调试程序可能会在同一进程中的 DEs在同一线程上运行。

 SDM 通常充当一种委派机制，但它可能充当广播机制。 例如，在表达式计算期间 SDM 充当广播的机制来通知所有 DEs 它们可以在指定的线程上运行代码。 同样，当 SDM 收到 stopping 事件，其广播到应停止运行的程序。 当调用一个步骤时，SDM 广播的程序，它们可以继续运行。 此外为每个 DE 广播断点。

 SDM 不会跟踪当前程序、 线程或堆栈帧。 进程、 程序和线程信息发送到与特定的调试事件结合使用 SDM。

## <a name="see-also"></a>请参阅
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [调试器组件](../../extensibility/debugger/debugger-components.md)
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)