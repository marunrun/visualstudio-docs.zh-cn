---
title: 表达式评估的示例实现 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
- expression evaluation, examples
ms.assetid: 2a5f04b8-6c65-4232-bddd-9093653a22c4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cf994a61ed9283463cd01aa468018f6acce5e209
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713103"
---
# <a name="sample-implementation-of-expression-evaluation"></a>表达式计算的样本实现
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 对于**监视**窗口表达式，Visual Studio 调用[ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)生成[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)对象。 `IDebugExpressionContext2::ParseText`实例化表达式赋值器 （EE） 并调用[Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)获取[IDebugParsed 表达式](../../extensibility/debugger/reference/idebugparsedexpression.md)对象。

 执行`IDebugExpressionEvaluator::Parse`以下任务：

1. [仅C++]分析表达式以查找错误。

2. 实例化运行`IDebugParsedExpression`接口并在类中存储`CParsedExpression`要解析的表达式的类（在此示例中称为）。

3. 从`IDebugParsedExpression``CParsedExpression`对象返回接口。

> [!NOTE]
> 在 MyCEE 示例之后和其中的示例中，表达式赋值器不会将分析与评估分开。

## <a name="managed-code"></a>托管代码
 以下代码显示了托管代码中的`IDebugExpressionEvaluator::Parse`实现。 此版本的方法将解析延迟到[EvaluateSync，](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)因为用于分析的代码也会同时计算（请参阅[评估 Watch 表达式](../../extensibility/debugger/evaluating-a-watch-expression.md)）。

```csharp
namespace EEMC
{
    public class CParsedExpression : IDebugParsedExpression
    {
        public HRESULT Parse(
                string                 expression,
                uint                   parseFlags,
                uint                   radix,
            out string                 errorMessage,
            out uint                   errorPosition,
            out IDebugParsedExpression parsedExpression)
        {
            errorMessage = "";
            errorPosition = 0;

            parsedExpression =
                new CParsedExpression(parseFlags, radix, expression);
            return COM.S_OK;
        }
    }
}
```

## <a name="unmanaged-code"></a>非托管代码
以下代码是在非托管代码`IDebugExpressionEvaluator::Parse`中的实现。 此方法调用帮助器函数`Parse`， 以解析表达式并检查错误，但此方法忽略生成的值。 正式计算延迟到[评估同步](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)，在计算表达式时解析表达式（请参阅[评估观察表达式](../../extensibility/debugger/evaluating-a-watch-expression.md)）。

```cpp
STDMETHODIMP CExpressionEvaluator::Parse(
        in    LPCOLESTR                 pszExpression,
        in    PARSEFLAGS                flags,
        in    UINT                      radix,
        out   BSTR                     *pbstrErrorMessages,
        inout UINT                     *perrorCount,
        out   IDebugParsedExpression  **ppparsedExpression
    )
{
    if (pbstrErrorMessages == NULL)
        return E_INVALIDARG;
    else
        *pbstrErrormessages = 0;

    if (pparsedExpression == NULL)
        return E_INVALIDARG;
    else
        *pparsedExpression = 0;

    if (perrorCount == NULL)
        return E_INVALIDARG;

    HRESULT hr;
    // Look for errors in the expression but ignore results
    hr = ::Parse( pszExpression, pbstrErrorMessages );
    if (hr != S_OK)
        return hr;

    CParsedExpression* pparsedExpr = new CParsedExpression( radix, flags, pszExpression );
    if (!pparsedExpr)
        return E_OUTOFMEMORY;

    hr = pparsedExpr->QueryInterface( IID_IDebugParsedExpression,
                                      reinterpret_cast<void**>(ppparsedExpression) );
    pparsedExpr->Release();

    return hr;
}
```

## <a name="see-also"></a>请参阅
- [评估"监视"窗口表达式](../../extensibility/debugger/evaluating-a-watch-window-expression.md)
- [评估监视表达式](../../extensibility/debugger/evaluating-a-watch-expression.md)
