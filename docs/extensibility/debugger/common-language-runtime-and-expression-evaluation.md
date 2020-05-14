---
title: 通用语言运行时和表达式计算 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, and common language runtime
ms.assetid: b36c1eb5-1aaf-48a6-b287-ee7a273d2b1c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 013579473189dd9310501b76d2de0d5cf6fa5822
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739121"
---
# <a name="common-language-runtime-and-expression-evaluation"></a>通用语言运行时和表达式计算
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 面向通用语言运行时 （CLR） 的编译器（如 Visual Basic 和 C#（发音为 C-sharp））生成 Microsoft 中间语言 （MSIL），后者后来被编译为本机代码。 CLR 提供调试引擎 （DE） 来调试生成的代码。 如果您计划将专有编程语言集成到 Visual Studio IDE 中，您可以选择编译到 MSIL，因此不必编写自己的 DE。 但是，您必须编写一个表达式赋值器 （EE），该表达式评估器能够评估编程语言上下文中的表达式。

## <a name="discussion"></a>讨论区
 通常对计算机语言表达式进行分析以生成一组数据对象和一组用于操作它们的运算符。 例如，可以分析表达式"A+B"以将添加运算符 （+） 应用于数据对象"A"和"B"，这可能导致另一个数据对象。 数据对象、运算符及其关联的总集通常以树的形式在程序中表示，其中运算符位于树的节点处，数据对象位于分支。 分解为树形的表达式通常称为解析树。

 分析表达式后，将调用符号提供程序 （SP） 以评估每个数据对象。 例如，如果"A"在多种方法中同时定义，则问题"哪个 A？ 必须先回答，然后才能确定 A 的值。 SP 返回的答案类似于"第五堆栈帧上的第三项"或"A 是 50 字节，超出分配给此方法的静态内存的开头。

 除了为程序本身生成 MSIL 外，CLR 编译器还可以生成非常描述性的调试信息，这些信息写入程序数据库 *（.pdb*） 文件中。 只要专有语言编译器生成与 CLR 编译器相同的格式的调试信息，CLR 的 SP 就能标识该语言的命名数据对象。 标识命名数据对象后，EE 使用活页夹对象将数据对象关联（或绑定）到保存该对象值的内存区域。 然后，DE 可以获取或设置数据对象的新值。

 专有编译器可以通过调用`ISymbolWriter`接口（在命名空间`System.Diagnostics.SymbolStore`中的 .NET 框架中定义）来提供 CLR 调试信息。 通过编译到 MSIL 并通过这些接口编写调试信息，专有编译器可以使用 CLR DE 和 SP。 这大大简化了将专有语言集成到可视化工作室 IDE 中。

 当 CLR DE 调用专有 EE 以评估表达式时，DE 向 EE 提供 SP 和活页夹对象的接口。 因此，编写基于 CLR 的调试引擎意味着只需实现适当的表达式赋值器接口;CLR 负责绑定和符号处理。

## <a name="see-also"></a>请参阅
- [编写 CLR 表达式赋值器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
