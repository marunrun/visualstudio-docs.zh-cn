---
title: 评估上下文 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, context
ms.assetid: 008a20c7-1b27-4013-bf96-d6a3f510da02
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b6a3d74c26b6ca94e0a4052df4810e407313a6cd
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66315506"
---
# <a name="evaluation-context"></a>评估上下文
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 当调试引擎 (DE) 调用表达式计算器 (EE) 三个参数，传递给[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)确定用于查找和评估符号，上下文下, 表中所示。

## <a name="arguments"></a>自变量

|参数|描述|
|--------------|-----------------|
|`pSymbolProvider`|[IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)接口指定的符号处理程序 (SH) 要用来标识该符号。|
|`pAddress`|[IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)指定当前执行点的接口。 此接口查找包含要执行的代码的方法。|
|`pBinder`|[IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)查找值和类型的给定名称的符号的接口。|

 `IDebugParsedExpression::EvaluateSync` 返回[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)表示生成的值和其类型的接口。

## <a name="see-also"></a>请参阅
- [键表达式计算器接口](../../extensibility/debugger/key-expression-evaluator-interfaces.md)
- [显示局部](../../extensibility/debugger/displaying-locals.md)
- [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)