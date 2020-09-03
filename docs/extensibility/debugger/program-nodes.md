---
title: 程序节点 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738220"
---
# <a name="program-nodes"></a>程序节点
在调试程序体系结构中， *程序节点*：

- 是对程序的轻型说明。

- 可以标识自身及其正在运行的进程。 程序节点可以附加到、从中分离出来，并描述调试引擎 (创建它的) （如果有）。

- 由 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) 接口表示，通常由 DE 或端口创建。 通过调用 [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)将程序节点添加到端口。 将程序节点添加到端口时，它会被添加到包含此程序节点所表示的程序的进程中。

  在调试会话启动之后的某个时间段，根据调试包的实现，程序节点用于创建相应的程序。 查询进程时，会枚举程序，每个程序节点各有一个。

  将程序附加到之前，IDE 只需要程序的轻型说明。 可以从程序节点获取此信息。 将程序附加到后，IDE 将显示更多详细信息，如程序中运行的所有线程的列表。 此信息是从程序本身获取的。

## <a name="see-also"></a>另请参阅
- [计划](../../extensibility/debugger/programs.md)
- [进程](../../extensibility/debugger/processes.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
