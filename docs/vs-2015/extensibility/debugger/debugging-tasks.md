---
title: 调试任务 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], tasks
ms.assetid: 5d60e9e8-305e-4a48-829f-b9440fc8af7b
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f4a8a9879bce6d91448bb4f29b842328ab56bb97
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200615"
---
# <a name="debugging-tasks"></a>调试任务
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

若要调试程序，它必须启动，调试引擎 (DE) 必须附加到它，或者 DE 必须附加到先前启动的程序。 附加完以后，DE 必须生成某些启动事件。 在响应中，尝试绑定在 IDE 中设置断点调试包。 当程序达到绑定的断点时，它会中止并等待用户输入。  
  
## <a name="in-this-section"></a>本节内容  
 [安全问题](../../extensibility/debugger/security-issues.md)  
 讨论调试的程序所需的安全步骤。  
  
 [启动程序](../../extensibility/debugger/launching-a-program.md)  
 提供有关如何指定 DE，后者调用操作系统来启动程序的分步说明。  
  
 [直接附加到程序](../../extensibility/debugger/attaching-directly-to-a-program.md)  
 描述用于调试的程序已在运行的进程中的过程。  
  
 [启动后发送启动事件](../../extensibility/debugger/sending-startup-events-after-a-launch.md)  
 列出 DE 附加到程序中，直到该程序在主入口点且已准备就绪以进行调试后发生的事件。  
  
 [控制执行](../../extensibility/debugger/control-of-execution.md)  
 介绍了如何 DE 通常情况下发送的入口点事件、 加载完成的事件或停止事件，视情况而定。  
  
 [绑定断点](../../extensibility/debugger/binding-breakpoints.md)  
 描述如何，如果用户设置一个断点，则 IDE 将编写请求和提示调试会话才能创建断点。  
  
 [计算表达式](../../extensibility/debugger/evaluating-expressions.md)  
 介绍如何创建表达式和表达式进行求值时，会发生什么情况。  
  
 [可视化和查看数据](../../extensibility/debugger/visualizing-and-viewing-data.md)  
 说明表达式计算器 (EE) 如何支持类型可视化工具和自定义查看器。  
  
## <a name="related-sections"></a>相关章节  
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)  
 描述调试的主要体系结构概念。  
  
 [调试器组件](../../extensibility/debugger/debugger-components.md)  
 概述 Visual Studio 调试组件，包括 DE、 EE 和符号处理程序 (SH)。  
  
 [调试器上下文](../../extensibility/debugger/debugger-contexts.md)  
 介绍了 DE 方式同时代码、 文档和表达式计算上下文中。 介绍的三个上下文、 位置、 位置或与它相关评估每个。  
  
## <a name="see-also"></a>请参阅  
 [入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
