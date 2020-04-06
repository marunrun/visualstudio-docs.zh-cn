---
title: 调试任务 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], tasks
ms.assetid: 5d60e9e8-305e-4a48-829f-b9440fc8af7b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d41f53ab1392ea3c31908faf65a871fa100fbb3f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738954"
---
# <a name="debug-tasks"></a>调试任务
要调试程序，必须启动该程序，并且必须将调试引擎 （DE） 附加到它，否则 DE 必须附加到以前启动的程序。 附加后，DE 必须生成某些启动事件。 作为响应，调试包尝试绑定在 IDE 中设置的断点。 当程序达到绑定断点时，它将停止并等待用户输入。

## <a name="in-this-section"></a>在本节中
 [安全问题](../../extensibility/debugger/security-issues.md)讨论调试程序所需的安全步骤。

 [启动程序](../../extensibility/debugger/launching-a-program.md)提供有关如何指定 DE 的分步说明，该 DE 调用操作系统启动程序。

 [直接附加到程序](../../extensibility/debugger/attaching-directly-to-a-program.md)描述用于在已运行的进程中调试程序的过程。

 [启动后发送启动事件](../../extensibility/debugger/sending-startup-events-after-a-launch.md)列出 DE 附加到程序后发生的事件，直到程序位于其主要入口点并准备好进行调试。

 [执行控制](../../extensibility/debugger/control-of-execution.md)说明 DE 通常如何根据具体情况发送入口点事件、负载完成事件或停止事件。

 [绑定断点](../../extensibility/debugger/binding-breakpoints.md)描述如果用户设置断点，IDE 如何制定请求并提示调试会话创建断点。

 [计算表达式](../../extensibility/debugger/evaluating-expressions.md)说明如何创建表达式以及计算表达式时会发生什么情况。

 [可视化和查看数据](../../extensibility/debugger/visualizing-and-viewing-data.md)说明表达式赋值器 （EE） 如何支持类型可视化器和自定义查看器。

## <a name="related-sections"></a>相关章节
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)描述主要的调试体系结构概念。

 [调试器组件](../../extensibility/debugger/debugger-components.md)提供 Visual Studio 调试组件的概述，其中包括 DE、EE 和符号处理程序 （SH）。

 [调试器上下文](../../extensibility/debugger/debugger-contexts.md)说明 DE 如何在代码、文档和表达式计算上下文中同时运行。 描述三个上下文中的每一个与它相关的位置、位置或评估。

## <a name="see-also"></a>请参阅
 [入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
