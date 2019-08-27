---
title: 公共语言运行时和表达式计算 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, and common language runtime
ms.assetid: b36c1eb5-1aaf-48a6-b287-ee7a273d2b1c
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b75cb1b0604f3611c0e51c6f458939433d2a5470
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383529"
---
# <a name="common-language-runtime-and-expression-evaluation"></a>公共语言运行时和表达式计算
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 编译器，如 Visual Basic 和 C# （读作 c-sharp），面向公共语言运行时 (CLR)，生成 Microsoft 中间语言 (MSIL)，这是更高版本编译为本机代码。 CLR 提供调试引擎 (DE) 生成的代码进行调试。 如果你打算将专有的编程语言集成到 Visual Studio IDE，您可以选择将编译为 MSIL 并因此不需要编写您自己 DE。 但是，您将必须编写能够计算上下文中的编程语言的表达式的表达式计算器 (EE)。  
  
## <a name="discussion"></a>讨论  
 通常，分析计算机语言表达式，以生成一组数据对象和一组用来对其进行处理的运算符。 例如，"A + B"可能会进行分析，以应用加法运算符 （+） 的数据的表达式的对象"A"和"B"可能会导致另一个数据对象。 数据对象、 运算符和其关联的总一最常在程序中表示为一个树，并在树的节点上的运算符和分支的数据对象。 一个表达式，被分解为树的形式通常称为分析的树。  
  
 一旦已分析表达式，被调用符号提供程序 (SP) 来计算每个数据对象。 例如，如果同时在多个方法，则问题定义"A"，则"的 A？" 可以确定一个的值之前必须回答。 返回由 SP 的答案是类似于"第五个堆栈帧上的第三个项"或者"A 的 50 个字节，超出的静态内存开始分配给此方法。"  
  
 除了为程序本身生成 MSIL，CLR 编译器还可以生成说明性很强的调试信息写入到程序数据库 (.pdb) 文件。 只要专有语言编译器生成调试信息放在与 CLR 编译器相同的格式，CLR 的 SP 是无法识别语言的名为数据对象。 一旦已确定的已命名的数据对象，EE 使用联编程序对象相关联 （或绑定） 的数据对象到的内存区域中保留该对象的值。 然后，DE 可以获取或设置数据对象的新值。  
  
 专有编译器可以提供 CLR 调试信息通过调用`ISymbolWriter`接口 (在.NET Framework 中的命名空间中定义`System.Diagnostics.SymbolStore`)。 专有编译器可以编译为 MSIL 和写入调试信息，通过这些接口，通过使用 CLR DE 和 sp。 这极大地简化了将专有语言集成到 Visual Studio IDE。  
  
 当 CLR DE 调用专有 EE 计算的表达式时，DE 提供 EE 和 SP 和联编程序对象的接口。 因此，编写基于 CLR 的调试引擎表示是只需实现适当的表达式计算器接口;CLR 负责的绑定和处理您的符号。  
  
## <a name="see-also"></a>请参阅  
 [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
