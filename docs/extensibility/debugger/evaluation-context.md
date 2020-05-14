---
title: 评估上下文 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, context
ms.assetid: 008a20c7-1b27-4013-bf96-d6a3f510da02
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5e3d02bd652d6c46b5aabe00e049e425f0921c27
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738797"
---
# <a name="evaluation-context"></a>评估上下文
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 当调试引擎 （DE） 调用表达式赋值器 （EE） 时，传递给[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)的三个参数决定了查找和评估符号的上下文，如下表所示。

## <a name="arguments"></a>自变量

|参数|描述|
|--------------|-----------------|
|`pSymbolProvider`|[IDebugSymbolProvider 接口](../../extensibility/debugger/reference/idebugsymbolprovider.md)，用于指定用于标识符号的符号处理程序 （SH）。|
|`pAddress`|指定当前执行点的[IDebug 地址](../../extensibility/debugger/reference/idebugaddress.md)接口。 此接口查找包含要执行的代码的方法。|
|`pBinder`|[IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)接口，用于查找给定符号名称的值和类型。|

 `IDebugParsedExpression::EvaluateSync`返回表示结果值及其类型的[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)接口。

## <a name="see-also"></a>请参阅
- [键表达式赋值器接口](../../extensibility/debugger/key-expression-evaluator-interfaces.md)
- [显示本地变量](../../extensibility/debugger/displaying-locals.md)
- [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)
