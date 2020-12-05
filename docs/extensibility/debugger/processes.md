---
title: 进程 |Microsoft Docs
description: 本文介绍 Visual Studio 的调试器结构中的进程的定义和角色。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], processes
ms.assetid: a6a1efdc-b243-40c8-a778-6f69f6b018be
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4a707d62443004795824c8bd437c29802635cf41
ms.sourcegitcommit: 42981ace63c0f2b087de5703ca76b8dcdd93a719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2020
ms.locfileid: "96606497"
---
# <a name="processes"></a>进程
在调试程序体系结构中， *进程*：

- 是一组程序的容器。 它与 Windows 进程非常相似，后者是一组线程的容器。

- 可以按名称、标识符或物理标识符来标识自身。

- 可以枚举所有正在运行的程序 (及其线程) 。

- 可以描述自身、运行它的端口以及包含它的计算机。

- 可以创建一个或多个程序、终止它创建的任何程序或导致程序停止。

- 由 [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md) 接口表示，该接口在进程启动时创建。 进程由会话调试管理器 (SDM) 或 [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)启动。

  调试包可以通过调用 [attach](../../extensibility/debugger/reference/idebugprocess2-attach.md)将调试引擎附加到进程 (取消) ，这意味着它会附加到可处理的进程中运行的所有可能的程序。 例如，如果公共语言运行时将附加到某个进程，则它仅附加到运行托管代码的程序。

## <a name="see-also"></a>请参阅
- Programs 
- [线程](../../extensibility/debugger/threads.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [调试包](../../extensibility/debugger/debug-package.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)
- [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [附加](../../extensibility/debugger/reference/idebugprocess2-attach.md)
