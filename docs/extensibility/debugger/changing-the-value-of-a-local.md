---
title: 更改本地 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, changing values programmatically
ms.assetid: 8407d3df-d38a-4328-82d1-98084bef43ec
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 565ae9f27b9f5a113e51520724f525599ad5eda7
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904269"
---
# <a name="change-the-value-of-a-local"></a>更改本地的值
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅[clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 在 "**局部变量**" 窗口的 "值" 字段中键入新值时，调试包将该字符串作为类型传递到表达式计算器（EE）。 EE 计算此字符串，其中可以包含简单值或表达式，并将生成的值存储在关联的本地中。

 这是更改本地的值的过程概述：

1. 用户输入新值后，Visual Studio 将对与本地关联的[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)对象调用[SetValueAsString](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md) 。

2. `IDebugProperty2::SetValueAsString` 执行下列任务：

   1. 计算用于生成值的字符串。

   2. 绑定关联的[IDebugField](../../extensibility/debugger/reference/idebugfield.md)对象以获取[IDebugObject](../../extensibility/debugger/reference/idebugobject.md)对象。

   3. 将值转换为一系列字节。

   4. 调用[SetValue](../../extensibility/debugger/reference/idebugobject-setvalue.md)将值的字节放入内存中，以便正在调试的程序可以访问它们。

3. Visual Studio 将刷新**局部变量**显示（有关详细信息，请参阅[显示局部变量](../../extensibility/debugger/displaying-locals.md)）。

   此过程还用于更改 "**监视**" 窗口中变量的值，只不过它是 `IDebugProperty2` 与使用的本地值（而不是 `IDebugProperty2` 与本地关联的对象关联）关联的对象。

## <a name="in-this-section"></a>本节内容
 [更改值的示例实现](../../extensibility/debugger/sample-implementation-of-changing-values.md)使用 MyCEE 示例来逐步完成更改值的过程。

## <a name="see-also"></a>另请参阅
- [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [显示局部变量](../../extensibility/debugger/displaying-locals.md)
