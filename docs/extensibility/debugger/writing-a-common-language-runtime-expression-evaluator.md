---
title: 编写通用语言运行时表达式赋值器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators, tutorial
- expression evaluation, samples
- debugging [Debugging SDK], expression evaluators tutorial
ms.assetid: bd79d57f-8e0a-4e14-a417-0b1de28fa1b2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4e46eaef395a7c66792662b3c5d4b9fbad419dfb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712327"
---
# <a name="writing-a-common-language-runtime-expression-evaluator"></a>编写通用语言运行时表达式赋值器
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表达式赋值器 （EE） 是调试引擎 （DE） 的一部分，用于处理生成要调试的代码的编程语言的语法和语义。 表达式必须在编程语言的上下文中计算。 例如，在某些语言中，表达式"A+B"表示"A 和 B 的总和"。 在其他语言中，相同的表达式可能表示"A 或 B"。 因此，必须为生成要在 Visual Studio IDE 中调试的对象代码的每个编程语言编写单独的 EE。

 Visual Studio 调试包的某些方面必须在编程语言的上下文中解释代码。 例如，当执行在断点停止时，必须计算并显示用户键入到**Watch**窗口中的任何表达式。 用户可以通过在 **"监视"** 窗口或 **"立即"** 窗口中键入表达式来更改本地变量的值。

## <a name="in-this-section"></a>在本节中
 [通用语言运行时和表达式计算](../../extensibility/debugger/common-language-runtime-and-expression-evaluation.md)说明在将专有编程语言集成到 Visual Studio IDE 中时，编写能够评估专有语言上下文中表达式的 EE 允许您编译到 Microsoft 中间语言 （MSIL），而无需编写调试引擎。

 [表达式赋值器体系结构](../../extensibility/debugger/expression-evaluator-architecture.md)讨论如何实现所需的 EE 接口并调用通用语言运行时符号提供程序 （SP） 和粘合剂接口。

 [注册表达式赋值器](../../extensibility/debugger/registering-an-expression-evaluator.md)请注意，EE 必须将自己注册为具有通用语言运行时和 Visual Studio 运行时环境的类工厂。

 [实现表达式赋值器](../../extensibility/debugger/implementing-an-expression-evaluator.md)描述计算表达式的过程如何包括调试引擎 （DE）、符号提供程序 （SP）、活页器对象和表达式赋值器 （EE）。

 [显示局部变量](../../extensibility/debugger/displaying-locals.md)描述调试包在执行暂停时如何调用 DE 来获取本地变量和参数的列表。

 [评估监视窗口表达式](../../extensibility/debugger/evaluating-a-watch-window-expression.md)记录 Visual Studio 调试包如何调用 DE 以确定其监视列表中每个表达式的当前值。

 [更改本地值](../../extensibility/debugger/changing-the-value-of-a-local.md)说明在更改局部变量的值时，"局部变量"窗口的每一行都有一个关联的对象，该对象提供本地的名称、类型和当前值。

 [实现类型可视化器和自定义查看器](../../extensibility/debugger/implementing-type-visualizers-and-custom-viewers.md)说明需要由哪个组件实现哪个接口来支持类型可视化器和自定义查看器。

## <a name="see-also"></a>请参阅
 [可视化工作室调试器可扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
