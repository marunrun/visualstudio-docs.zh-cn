---
title: 调试器概念 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK]
ms.assetid: 2d371d38-f1a0-4a9a-8ea3-100e8c0149b7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f1d9905281c83287b8b54f57a233c2056462226f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66345924"
---
# <a name="debugger-concepts"></a>调试器概念
若要在 Visual Studio 调试包上构建，需要熟悉在设计包中使用的体系结构概念。

## <a name="in-this-section"></a>本节内容
 [调试会话](../../extensibility/debugger/debug-session.md)说明调试体系结构中的会话的作用。

 [服务器](../../extensibility/debugger/servers-visual-studio-sdk.md)哪台服务器是在抽象和物理条款中的调试体系结构方面的定义。

 [端口供应商](../../extensibility/debugger/port-suppliers.md)端口提供程序是在调试体系结构方面的定义。

 [端口](../../extensibility/debugger/ports.md)哪些端口是在调试体系结构方面的定义。

 [进程](../../extensibility/debugger/processes.md)哪些进程是在调试体系结构方面的定义。

 [程序节点](../../extensibility/debugger/program-nodes.md)定义方面调试体系结构，包括如何它可以标识本身和它正在运行中的进程的程序节点。

 [程序](../../extensibility/debugger/programs.md)定义在调试体系结构方面的程序。

 [线程](../../extensibility/debugger/threads.md)定义线程在调试体系结构方面的特征。

 [堆栈帧](../../extensibility/debugger/stack-frames.md)定义在调试体系结构方面的堆栈帧。 堆栈帧是堆栈提供一个线程的执行上下文的抽象。

 [模块](../../extensibility/debugger/modules.md)定义模块，在调试的代码，如可执行文件或 DLL 的物理容器体系结构方面。

 [断点](../../extensibility/debugger/breakpoints-visual-studio-sdk.md)定义三种类型的断点，挂起、 绑定和错误 — 在调试体系结构方面。

## <a name="related-sections"></a>相关章节
 [调试器上下文](../../extensibility/debugger/debugger-contexts.md)介绍了调试引擎 (DE) 的运行方式同时代码、 文档和表达式计算上下文。 介绍的三个上下文、 位置、 位置或与它相关评估每个。

 [调试器组件](../../extensibility/debugger/debugger-components.md)提供 Visual Studio 调试组件，包括调试引擎 (DE)、 表达式计算器 (EE) 和符号处理程序 (SH) 的概述。

 [调试任务](../../extensibility/debugger/debugging-tasks.md)包含指向各种调试任务，如启动程序和计算表达式。