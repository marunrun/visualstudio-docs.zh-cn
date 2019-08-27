---
title: 调试器上下文 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 79808036-b680-4e4c-9c61-4ed43aa11323
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 011999929fd4cb1508bf4958629e622684f35739
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66345999"
---
# <a name="debugger-contexts"></a>调试器上下文
在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试，调试引擎 (DE) 同时在内运行多个不同的上下文中，按如下所示：

- 代码上下文，其中描述了用于控制程序执行流中的当前位置。

- 文档上下文或位置，其中描述了源文档中的当前位置。

- 表达式计算上下文描述中的表达式求值将发生的上下文。

## <a name="in-this-section"></a>本节内容
 [代码上下文](../../extensibility/debugger/code-context.md)讨论代码上下文为今天的运行时体系结构中与非传统的语言，其中代码可能不表示的说明，但某些其他方式的程序的指令流中的地址。

 [文档位置](../../extensibility/debugger/document-position.md)定义在 Visual Studio 调试通过源文件中的位置的抽象，因为识别到 IDE 中的文档位置。

 [文档上下文](../../extensibility/debugger/document-context.md)哪些文档上下文表示在 Visual Studio 调试与源文件相关的讨论。 此外讨论了符号处理程序如何映射到文档上下文的代码上下文。

 [表达式计算上下文](../../extensibility/debugger/expression-evaluation-context.md)提供有关在 Visual Studio 中的表达式计算上下文的信息。 例如，与堆栈帧关联表达式计算上下文提供有关评估本地变量、 方法参数和类成员的上下文。

## <a name="related-sections"></a>相关章节
 [调试概念](../../extensibility/debugger/debugger-concepts.md)介绍了调试的主要体系结构概念。

 [调试组件](../../extensibility/debugger/debugger-components.md)提供 Visual Studio 调试组件，包括调试引擎 (DE)、 表达式计算器 (EE) 和符号处理程序 (SH) 的概述。

 [调试任务](../../extensibility/debugger/debugging-tasks.md)包含指向各种调试任务，如启动程序和计算表达式。