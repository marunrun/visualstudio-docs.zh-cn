---
title: 程序节点 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- program nodes, debugging context
- debugging [Debugging SDK], program nodes
- program nodes, adding
- program nodes, superceding
ms.assetid: 1c5a5c13-c14d-42c3-af11-4c63f1032c8d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2943f74c7316495be93c2f5c20998ffa685f5d01
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738220"
---
# <a name="program-nodes"></a>程序节点
在调试器体系结构中，*程序节点*：

- 是程序的轻量级描述。

- 可以标识自身及其正在运行的进程。 可以附加到、分离程序节点并描述创建它的调试引擎 （DE）（如果有）。

- 由[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)接口表示，通常由 DE 或端口创建。 程序节点通过调用[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)添加到端口。 将程序节点添加到端口时，该节点将添加到包含此程序节点表示的程序的进程。

  调试会话启动后的某个时间，根据调试包的实现，程序节点用于创建相应的程序。 当查询进程的程序时，将枚举程序，每个程序节点一个程序。

  在将程序附加到之前，IDE 只需要该程序的轻量级说明。 此信息可以从程序节点获取。 附加程序后，IDE 将显示更详细的信息，例如程序中运行的所有线程的列表。 此信息是从程序本身获取的。

## <a name="see-also"></a>请参阅
- [程序](../../extensibility/debugger/programs.md)
- [过程](../../extensibility/debugger/processes.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
