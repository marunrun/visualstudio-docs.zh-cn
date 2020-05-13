---
title: 调试器概念 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738983"
---
# <a name="debugger-concepts"></a>调试器概念
要构建 Visual Studio 调试包，您需要熟悉设计包时使用的体系结构概念。

## <a name="in-this-section"></a>在本节中
 [调试会话](../../extensibility/debugger/debug-session.md)解释会话在调试体系结构中的角色。

 [服务器](../../extensibility/debugger/servers-visual-studio-sdk.md)以抽象和物理术语定义服务器在调试体系结构方面的内容。

 [港口供应商](../../extensibility/debugger/port-suppliers.md)定义端口供应商在调试体系结构方面的内容。

 [端口](../../extensibility/debugger/ports.md)定义端口在调试体系结构方面是什么。

 [流程](../../extensibility/debugger/processes.md)定义进程在调试体系结构方面是什么。

 [程序节点](../../extensibility/debugger/program-nodes.md)定义程序节点的调试体系结构，包括它如何标识自身及其正在运行的进程。

 [计划](../../extensibility/debugger/programs.md)根据调试体系结构定义程序。

 [螺纹](../../extensibility/debugger/threads.md)定义线程在调试体系结构方面的特征。

 [堆叠帧](../../extensibility/debugger/stack-frames.md)根据调试体系结构定义堆栈帧。 堆栈框架是提供线程执行上下文的堆栈的抽象。

 [模块](../../extensibility/debugger/modules.md)在调试体系结构方面，将模块定义为代码的物理容器，如可执行文件或 DLL。

 [断点](../../extensibility/debugger/breakpoints-visual-studio-sdk.md)定义三种类型的断点 - 挂起、绑定和错误 - 在调试体系结构方面。

## <a name="related-sections"></a>相关章节
 [调试器上下文](../../extensibility/debugger/debugger-contexts.md)说明调试引擎 （DE） 如何在代码、文档和表达式评估上下文中同时运行。 描述三个上下文中的每一个与它相关的位置、位置或评估。

 [调试器组件](../../extensibility/debugger/debugger-components.md)提供可视化工作室调试组件的概述，其中包括调试引擎 （DE）、表达式赋值器 （EE） 和符号处理程序 （SH）。

 [调试任务](../../extensibility/debugger/debugging-tasks.md)包含指向各种调试任务的链接，例如启动程序和评估表达式。
