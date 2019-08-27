---
title: 更改局部值 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, changing values programmatically
ms.assetid: 8407d3df-d38a-4328-82d1-98084bef43ec
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 998200420cf2ec5e0b021a415cdb9d287b1362db
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349756"
---
# <a name="change-the-value-of-a-local"></a>更改局部值
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 值字段中键入新值时**局部变量**窗口中，调试程序包传递字符串，类型化的向表达式计算器 (EE)。 EE 计算此字符串，它可以包含一个简单的值或表达式，并将生成的值存储在关联的本地。

 这是过程的本地的更改值的概述：

1. 用户输入新值后，Visual Studio 会调用[SetValueAsString](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)上[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)与本地相关联的对象。

2. `IDebugProperty2::SetValueAsString` 执行下列任务：

   1. 计算要生成一个值的字符串。

   2. 将绑定相关联[IDebugField](../../extensibility/debugger/reference/idebugfield.md)对象，以获取[IDebugObject](../../extensibility/debugger/reference/idebugobject.md)对象。

   3. 将值转换为一系列字节。

   4. 调用[SetValue](../../extensibility/debugger/reference/idebugobject-setvalue.md)值的字节数放入内存，因此正在调试的程序可以访问它们。

3. Visual Studio 刷新**局部变量**显示 (请参阅[显示局部变量](../../extensibility/debugger/displaying-locals.md)有关详细信息)。

   此过程还用于更改中的变量的值**Watch**窗口中，但它是`IDebugProperty2`而不是使用该局部变量的值与关联的对象`IDebugProperty2`与本地相关联的对象本身。

## <a name="in-this-section"></a>本节内容
 [更改值的示例实现](../../extensibility/debugger/sample-implementation-of-changing-values.md)使用 MyCEE 样本来单步执行更改值的过程。

## <a name="see-also"></a>请参阅
- [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [显示局部](../../extensibility/debugger/displaying-locals.md)