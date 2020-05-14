---
title: 调试器上下文 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738971"
---
# <a name="debugger-contexts"></a>调试器上下文
在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试中，调试引擎 （DE） 在几个不同的上下文中同时运行，如下所示：

- 代码上下文，它描述程序执行流中的当前位置。

- 文档上下文或位置，用于描述源文档中的当前位置。

- 表达式计算上下文，它描述将进行表达式计算的上下文。

## <a name="in-this-section"></a>在本节中
 [代码上下文](../../extensibility/debugger/code-context.md)将代码上下文作为当今运行时体系结构中程序指令流中的地址讨论，而非传统语言则不由指令表示，但使用其他一些方法。

 [文档位置](../../extensibility/debugger/document-position.md)通过在源文件中的位置（如 IDE 已知）的抽象来定义 Visual Studio 调试中的文档位置。

 [文档上下文](../../extensibility/debugger/document-context.md)讨论可视化工作室调试中相对于源文件表示的文档上下文。 还讨论了符号处理程序如何将代码上下文映射到文档上下文。

 [表达式计算上下文](../../extensibility/debugger/expression-evaluation-context.md)提供有关可视化工作室中的表达式评估上下文的信息。 例如，与堆栈框架关联的表达式计算上下文提供用于评估局部变量、方法参数和类成员的上下文。

## <a name="related-sections"></a>相关章节
 [调试概念](../../extensibility/debugger/debugger-concepts.md)描述主要的调试体系结构概念。

 [调试组件](../../extensibility/debugger/debugger-components.md)提供 Visual Studio 调试组件的概述，其中包括调试引擎 （DE）、表达式赋值器 （EE） 和符号处理程序 （SH）。

 [调试任务](../../extensibility/debugger/debugging-tasks.md)包含指向各种调试任务的链接，例如启动程序和评估表达式。
