---
title: 程序 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], programs
- programs, debugging
ms.assetid: e1f955d8-95da-493b-837e-e97741a26d7e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d3fd1db5add74d2d94467e1f369916feb5f30d4a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738204"
---
# <a name="programs"></a>程序
在调试器体系结构中，*程序*：

- 是一组线程和一组模块的容器。 程序在 Windows 操作系统中没有单一类比。

     程序是一种子过程。 例如，在调试网站时，可以将脚本视为程序。 当脚本在脚本引擎进程中运行时，独立于其他脚本，但它也有自己的一组线程。 调试引擎 （DE） 附加到程序，而不是进程或线程。

- 可以标识自身及其正在运行的进程。 可以附加到程序，与创建它的 DE（如果有）分离并描述该程序。 程序还可以执行、停止、继续和终止。

- 可以枚举其所有线程。 程序还可以提供自己的拆解流，并可以枚举给定文档位置的所有代码上下文。

- 由[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)接口表示，在附加程序之前创建，或作为附加过程的一部分，具体取决于实现。 当端口枚举进程的程序时，每个程序都按照作为[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)的参数传递给的相应[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)接口创建。 虽然调试引擎还会创建`IDebugProgram2`接口来表示程序，但这些程序不是根据程序节点创建的。 DE`IDebugProgramNode2`创建的接口用于实际调试，而端口创建的接口仅用于发现进程中正在运行的程序。

## <a name="see-also"></a>请参阅
- [过程](../../extensibility/debugger/processes.md)
- [程序节点](../../extensibility/debugger/program-nodes.md)
- [模块](../../extensibility/debugger/modules.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [文档位置](../../extensibility/debugger/document-position.md)
- [代码上下文](../../extensibility/debugger/code-context.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
