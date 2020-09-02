---
title: 调试器上下文 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 79808036-b680-4e4c-9c61-4ed43aa11323
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 56825fe299147e60c5ed9dfcefa491a427ab59e4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738971"
---
# <a name="debugger-contexts"></a>调试器上下文
在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试中，调试引擎 (DE) 在多个不同的上下文中同时运行，如下所示：

- 代码上下文，描述程序的执行流中的当前位置。

- 文档上下文或位置，描述源文档中的当前位置。

- 表达式计算上下文，描述将在其中发生表达式求值的上下文。

## <a name="in-this-section"></a>本节内容
 [代码上下文](../../extensibility/debugger/code-context.md) 在当今的运行时体系结构与 nontraditional 的语言中，将代码上下文讨论为程序指令流中的一个地址，其中，代码可能不由说明表示，而是其他一些方法。

 [文档位置](../../extensibility/debugger/document-position.md) 在 Visual Studio 中定义文档位置，方法是通过将源文件中的位置抽象到 IDE 已知的方式进行调试。

 [文档上下文](../../extensibility/debugger/document-context.md) 讨论 Visual Studio 中与源文件相关的文档上下文表示的内容。 还讨论了符号处理程序如何将代码上下文映射到文档上下文。

 [表达式计算上下文](../../extensibility/debugger/expression-evaluation-context.md) 提供有关 Visual Studio 中的表达式计算上下文的信息。 例如，与堆栈帧关联的表达式计算上下文提供用于计算局部变量、方法参数和类成员的上下文。

## <a name="related-sections"></a>相关章节
 [调试概念](../../extensibility/debugger/debugger-concepts.md) 介绍主要调试体系结构概念。

 [调试组件](../../extensibility/debugger/debugger-components.md) 概述 Visual Studio 调试组件，其中包括调试引擎 (DE) 、expression 计算器 (EE) 以及符号处理程序 (SH) 。

 [调试任务](../../extensibility/debugger/debugging-tasks.md) 包含指向各种调试任务的链接，如启动程序和计算表达式。
