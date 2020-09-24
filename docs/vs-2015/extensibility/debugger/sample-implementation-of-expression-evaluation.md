---
title: 表达式计算的示例实现 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
- expression evaluation, examples
ms.assetid: 2a5f04b8-6c65-4232-bddd-9093653a22c4
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a7a19247b296d7e00a15051e75dd53536133c426
ms.sourcegitcommit: bccc6503542e1517e0e96a9f02f5a89d69c60c25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2020
ms.locfileid: "91147238"
---
# <a name="sample-implementation-of-expression-evaluation"></a>表达式计算的实现示例
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 对于 " **监视** 窗口" 表达式，Visual Studio 会调用 [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 来生成 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 对象。 `IDebugExpressionContext2::ParseText` 实例化表达式计算器 (EE) 并调用 [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) 来获取 [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) 对象。  
  
 此实现 `IDebugExpressionEvaluator::Parse` 执行以下任务：  
  
1. [仅限 c + +]分析表达式以查找错误。  
  
2. 实例化 `CParsedExpression` 在此示例中调用的类 () 实现 `IDebugParsedExpression` 接口，并在类中存储要分析的表达式。  
  
3. `IDebugParsedExpression`从对象返回接口 `CParsedExpression` 。  
  
> [!NOTE]
> 在以下示例中，在 MyCEE 示例中，表达式计算器不会将分析与计算分离。  
  
## <a name="managed-code"></a>托管代码  
 这是 `IDebugExpressionEvaluator::Parse` 托管代码中的的实现。 请注意，此版本的方法会将分析推迟到 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) ，因为用于分析的代码也会同时计算 (参阅 [计算监视表达式](../../extensibility/debugger/evaluating-a-watch-expression.md)) 。  
  
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
 这是 `IDebugExpressionEvaluator::Parse` 在非托管代码中实现的。 此方法调用 helper 函数 `Parse` 来分析表达式并检查是否有错误，但此方法忽略生成的值。 在计算表达式 (参阅) [计算监视表达式](../../extensibility/debugger/evaluating-a-watch-expression.md)时，将将正式计算延迟为[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) 。  
  
```cpp#  
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
  
## <a name="see-also"></a>另请参阅  
 [计算监视窗口表达式](../../extensibility/debugger/evaluating-a-watch-window-expression.md)   
 [计算监视表达式](../../extensibility/debugger/evaluating-a-watch-expression.md)
