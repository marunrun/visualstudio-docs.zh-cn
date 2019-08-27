---
title: IDebugParsedExpression | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugParsedExpression
helpviewer_keywords:
- IDebugParsedExpression interface
ms.assetid: be6486ed-b070-4898-95b1-58581bcb4447
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c56c0547d348c4fb3de387ac0ffce465b7bf5e90
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66311778"
---
# <a name="idebugparsedexpression"></a>IDebugParsedExpression
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口表示可供计算的已分析的表达式。

## <a name="syntax"></a>语法

```
IDebugParsedExpression : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 表达式计算器实现此接口来表示一个已分析的表达式，为准备好进行评估。

## <a name="notes-for-callers"></a>调用方的说明
 调用[分析](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugParsedExpression`。

|方法|描述|
|------------|-----------------|
|[EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)|已分析的表达式的计算结果。|

## <a name="remarks"></a>备注
 当调用方已准备好计算表达式时，它将调用[EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)返回[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) ，其中包含计算的结果。 评估，然后评估，使分析得出的表达式将计算多次分析，从而绕过分析该表达式的耗时的过程此由两部分方法。

## <a name="requirements"></a>要求
 标头： ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [分析](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)