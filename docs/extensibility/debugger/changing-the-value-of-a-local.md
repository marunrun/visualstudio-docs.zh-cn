---
title: 更改本地值 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, changing values programmatically
ms.assetid: 8407d3df-d38a-4328-82d1-98084bef43ec
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 98e40e4b6ea10bb6ff1242f23f1b6dd83ce0c0cd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739146"
---
# <a name="change-the-value-of-a-local"></a>更改本地值
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 在 **"局部变量"** 窗口的值字段中键入新值时，调试包会将字符串（键入）传递给表达式赋值器 （EE）。 EE 计算此字符串，该字符串可以包含简单值或表达式，并将结果值存储在关联的本地中。

 这是更改本地值的过程的概述：

1. 用户输入新值后，Visual Studio 会在与本地关联的[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)对象上调用[SetValueAsString。](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)

2. `IDebugProperty2::SetValueAsString` 执行以下任务：

   1. 评估要生成值的字符串。

   2. 绑定关联的[IDebugField](../../extensibility/debugger/reference/idebugfield.md)对象以获取[IDebugObject 对象](../../extensibility/debugger/reference/idebugobject.md)。

   3. 将值转换为一系列字节。

   4. 调用[SetValue](../../extensibility/debugger/reference/idebugobject-setvalue.md)将值的字节放入内存中，以便正在调试的程序可以访问它们。

3. 可视化工作室刷新 **"局部变量"** 显示（有关详细信息[，请参阅显示局部变量](../../extensibility/debugger/displaying-locals.md)）。

   此过程还用于更改**Watch**窗口中变量的值，只不过它是与所使用的局部变量的值关联的`IDebugProperty2`对象，而不是与本地本身关联的`IDebugProperty2`对象。

## <a name="in-this-section"></a>在本节中
 [更改值的示例实现](../../extensibility/debugger/sample-implementation-of-changing-values.md)使用 MyCEE 示例逐步完成更改值的过程。

## <a name="see-also"></a>请参阅
- [编写 CLR 表达式赋值器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [显示本地变量](../../extensibility/debugger/displaying-locals.md)
