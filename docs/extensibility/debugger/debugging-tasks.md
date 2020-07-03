---
title: 调试任务 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: overview
helpviewer_keywords:
- debugging [Debugging SDK], tasks
ms.assetid: 5d60e9e8-305e-4a48-829f-b9440fc8af7b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 070068853d962bdf9b209edb9410d33d46ccf853
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903558"
---
# <a name="debug-tasks"></a>调试任务
若要调试程序，必须启动该程序，必须将调试引擎（DE）附加到该程序，否则 DE 必须附加到以前启动的程序。 附加后，DE 必须生成特定的启动事件。 作为响应，调试包将尝试绑定 IDE 中设置的断点。 当程序到达绑定断点时，它会暂停并等待用户输入。

## <a name="in-this-section"></a>本节内容
 [安全问题](../../extensibility/debugger/security-issues.md)讨论调试程序所需的安全步骤。

 [启动程序](../../extensibility/debugger/launching-a-program.md)提供如何指定 DE 的分步说明，它调用操作系统来启动程序。

 [直接附加到程序](../../extensibility/debugger/attaching-directly-to-a-program.md)描述用于在已运行的进程中调试程序的过程。

 [启动后发送启动事件](../../extensibility/debugger/sending-startup-events-after-a-launch.md)列出在将 DE 附加到程序后发生的事件，直到程序进入其主入口点并准备好进行调试。

 [控制执行](../../extensibility/debugger/control-of-execution.md)说明如何根据具体的情况，操作通常发送入口点事件、加载完成事件或停止事件。

 [绑定断点](../../extensibility/debugger/binding-breakpoints.md)描述如何在用户设置断点时，IDE 形成请求并提示调试会话创建断点。

 [计算表达式](../../extensibility/debugger/evaluating-expressions.md)说明如何创建表达式以及在计算表达式时所发生的情况。

 [可视化和查看数据](../../extensibility/debugger/visualizing-and-viewing-data.md)说明表达式计算器（EE）如何支持类型可视化工具和自定义查看器。

## <a name="related-sections"></a>相关章节
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)介绍主要调试体系结构概念。

 [调试器组件](../../extensibility/debugger/debugger-components.md)概述 Visual Studio 调试组件，其中包括 DE、EE 和符号处理程序（SH）。

 [调试器上下文](../../extensibility/debugger/debugger-contexts.md)说明如何在代码、文档和表达式计算上下文中执行取消操作。 描述每个上下文的位置、位置或与之相关的计算。

## <a name="see-also"></a>另请参阅
 [入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
