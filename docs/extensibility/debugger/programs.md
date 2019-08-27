---
title: 程序 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], programs
- programs, debugging
ms.assetid: e1f955d8-95da-493b-837e-e97741a26d7e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e70a970aad250a30e19fd27ac3a47732952b3bf1
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351399"
---
# <a name="programs"></a>Programs
在调试器体系结构中，*程序*:

- 是一组线程和一组模块的容器。 程序在 Windows 操作系统中有任何单个的类比。

     程序是一种类型的子进程。 例如，调试网站时，脚本可视为程序。 脚本引擎进程脚本时，独立于其他脚本，它还具有自己的线程的一组。 调试引擎 (DE) 将附加到程序中，并且不给进程或线程。

- 可以标识本身和它正在运行中的进程。 程序可以附加、 分离，并介绍创建它，DE，如果有的话。 程序还可以执行、 停止、 继续，并会终止。

- 可以枚举所有线程。 程序还可以提供其自己的反汇编流，并可以枚举给定的文档位置的所有代码上下文。

- 为由[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)创建附加程序之前，或附加过程，具体取决于实现的接口。 每个程序时端口枚举进程的程序时，会创建根据相应[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)接口传递的参数作为[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)。 尽管的调试引擎还创建`IDebugProgram2`接口来表示程序，这些程序不会创建根据程序节点。 `IDebugProgramNode2`那些通过端口仅用于发现进程中运行哪些程序用于实现实际调试接口创建的部署。

## <a name="see-also"></a>请参阅
- [进程](../../extensibility/debugger/processes.md)
- [程序节点](../../extensibility/debugger/program-nodes.md)
- [模块](../../extensibility/debugger/modules.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [文档位置](../../extensibility/debugger/document-position.md)
- [代码上下文](../../extensibility/debugger/code-context.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)