---
title: 编写公共语言运行时表达式计算器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators, tutorial
- expression evaluation, samples
- debugging [Debugging SDK], expression evaluators tutorial
ms.assetid: bd79d57f-8e0a-4e14-a417-0b1de28fa1b2
caps.latest.revision: 24
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 961a4d646a61fedda381f9451902b3bcdcc956d6
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435280"
---
# <a name="writing-a-common-language-runtime-expression-evaluator"></a>编写公共语言运行时表达式计算器
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 表达式计算器 (EE) 是一个调试引擎 (DE)，处理语法的一部分并生成正在调试的代码的编程语言的语义。 必须在编程语言的上下文中计算表达式。 例如，在某些语言中，表达式"A + B"表示"之和 A 和 b。" 在其他语言，同一表达式可能意味着"或 B"。 因此，单独 EE 必须编写为在 Visual Studio IDE 中生成对象代码要调试每种编程语言。  
  
 Visual Studio 调试包的某些方面必须解释的编程语言的上下文中的代码。 例如，执行停止在断点处，键入该用户具有任何表达式**监视**必须计算并显示窗口。 此外，用户可以更改本地变量的值，通过键入到表达式**Watch**窗口或 into**即时**窗口。  
  
## <a name="in-this-section"></a>本节内容  
 [公共语言运行时和表达式计算](../../extensibility/debugger/common-language-runtime-and-expression-evaluation.md)  
 介绍了，将专用的编程语言集成到 Visual Studio IDE，编写 EE 能够计算表达式的上下文中的专有语言可编译为 Microsoft 中间语言 (MSIL)而无需编写调试引擎。  
  
 [表达式计算器体系结构](../../extensibility/debugger/expression-evaluator-architecture.md)  
 讨论如何实现所需的 EE 接口和调用的公共语言运行时符号提供程序 (SP) 和绑定器接口。  
  
 [注册表达式计算器](../../extensibility/debugger/registering-an-expression-evaluator.md)  
 说明 EE 必须将自身注册为使用公共语言运行时和 Visual Studio 运行时环境的类工厂。  
  
 [实现表达式计算器](../../extensibility/debugger/implementing-an-expression-evaluator.md)  
 介绍如何评估表达式的过程包含调试引擎 (DE)、 符号提供程序 (SP)、 联编程序对象和表达式计算器 (EE)。  
  
 [显示局部](../../extensibility/debugger/displaying-locals.md)  
 介绍如何操作，请时暂停执行，调试包调用 DE 来获取本地变量和参数的列表。  
  
 [计算监视窗口表达式](../../extensibility/debugger/evaluating-a-watch-window-expression.md)  
 介绍如何将 Visual Studio 调试包调用 DE 以确定其监视列表中的每个表达式的当前值。  
  
 [更改局部值](../../extensibility/debugger/changing-the-value-of-a-local.md)  
 说明，更改局部变量的值，在局部变量窗口的每一行都具有一个关联的对象，提供名称、 类型和局部变量的当前值。  
  
 [实现类型可视化工具和自定义查看器](../../extensibility/debugger/implementing-type-visualizers-and-custom-viewers.md)  
 说明哪个接口需要实现由哪些组件以支持类型可视化工具和自定义查看器。  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 调试器可扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
