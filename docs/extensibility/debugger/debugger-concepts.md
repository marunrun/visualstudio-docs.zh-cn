---
title: 调试器概念 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK]
ms.assetid: 2d371d38-f1a0-4a9a-8ea3-100e8c0149b7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9ad8a450f9e79c1d44b8e098c8a00bb4b816e1af
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738983"
---
# <a name="debugger-concepts"></a>调试器概念
若要在 Visual Studio 调试包上构建，需要熟悉设计包时使用的体系结构概念。

## <a name="in-this-section"></a>本节内容
 [调试会话](../../extensibility/debugger/debug-session.md) 说明会话在调试体系结构中的角色。

 [服务器](../../extensibility/debugger/servers-visual-studio-sdk.md) 定义服务器在抽象和物理术语方面的调试体系结构。

 [端口供应商](../../extensibility/debugger/port-suppliers.md) 定义端口供应商在调试体系结构方面的含义。

 [端口](../../extensibility/debugger/ports.md) 定义端口在调试体系结构方面的含义。

 [进程](../../extensibility/debugger/processes.md) 定义进程在调试体系结构方面的含义。

 [程序节点](../../extensibility/debugger/program-nodes.md) 根据调试体系结构定义一个程序节点，其中包括它如何识别自身及其正在运行的进程。

 [程序](../../extensibility/debugger/programs.md) 根据调试体系结构来定义程序。

 [线程](../../extensibility/debugger/threads.md) 定义线程在调试体系结构方面的特征。

 [堆栈帧](../../extensibility/debugger/stack-frames.md) 根据调试体系结构定义堆栈帧。 堆栈帧是提供线程执行上下文的堆栈抽象。

 [模块](../../extensibility/debugger/modules.md) 定义模块的调试体系结构，作为代码的物理容器，如可执行文件或 DLL。

 [断点](../../extensibility/debugger/breakpoints-visual-studio-sdk.md) 定义三种类型的断点：挂起、绑定和错误（在调试体系结构中）。

## <a name="related-sections"></a>相关章节
 [调试器上下文](../../extensibility/debugger/debugger-contexts.md) 说明调试引擎 (DE) 如何在代码、文档和表达式计算上下文中同时运行。 描述每个上下文的位置、位置或与之相关的计算。

 [调试器组件](../../extensibility/debugger/debugger-components.md) 概述 Visual Studio 调试组件，其中包括调试引擎 (DE) 、expression 计算器 (EE) 以及符号处理程序 (SH) 。

 [调试任务](../../extensibility/debugger/debugging-tasks.md) 包含指向各种调试任务的链接，如启动程序和计算表达式。
