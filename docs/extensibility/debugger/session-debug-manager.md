---
title: 会话调试管理器 |Microsoft Docs
description: 了解会话调试管理器，该管理器在多个计算机上管理多个进程中调试程序的多个调试引擎。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: d2c51b1fd345789cabbb9735621626ab7c2db993
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2020
ms.locfileid: "96845279"
---
# <a name="session-debug-manager"></a>会话调试管理器
会话调试管理器 (SDM) 管理任意数量的调试引擎)  (用于在多个进程中调试任意数量的程序的调试引擎。 除了成为调试引擎多路复用器外，SDM 还为 IDE 提供了一个统一的调试会话视图。

## <a name="session-debug-manager-operation"></a>会话调试管理器操作
 会话调试管理器 (SDM) 管理取消。 一台计算机上可以同时运行多个调试引擎。 为了多路复用 DEs，SDM 会包装来自 DEs 的多个接口，并将它们作为单个接口公开到 IDE。

 为了提高性能，某些接口不会进行多路复用。 相反，它们会直接在 DE 中使用，并且对这些接口的调用不会经过 SDM。 例如，用于内存、代码和文档上下文的接口不是多路复用的，因为它们引用特定的指令、内存或特定程序中由特定 DE 调试的文档。 此通信级别不需要进行任何其他的取消。

 这对于所有上下文都是如此。 对表达式求值上下文接口的调用会经历 SDM。 在表达式计算过程中，SDM 会包装它为 IDE 提供的 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 接口，因为在计算该表达式时，它可能涉及多个 DEs，这种情况可能是在同一线程上运行的同一进程中调试程序的。

 SDM 通常充当委托机制，但它可以充当广播机制。 例如，在表达式计算过程中，SDM 充当一种广播机制，用于通知所有 DEs 它们可在指定的线程上运行代码。 同样，当 SDM 收到停止事件时，它将广播到应停止运行的程序。 调用步骤时，SDM 会向程序广播，使其可以继续运行。 断点也会广播到每次取消。

 SDM 不跟踪当前程序、线程或堆栈帧。 进程、程序和线程信息与特定的调试事件一起发送到 SDM。

## <a name="see-also"></a>请参阅
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [调试器组件](../../extensibility/debugger/debugger-components.md)
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)
