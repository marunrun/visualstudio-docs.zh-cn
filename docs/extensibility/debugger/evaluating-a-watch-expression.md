---
title: 计算监视表达式 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, watch expressions
- watch expressions
ms.assetid: 8317cd52-6fea-4e8f-a739-774dc06bd44b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9a239e430338e88a0be4bc35ad1c357925f7d8f5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738851"
---
# <a name="evaluate-a-watch-expression"></a>计算监视表达式
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

当 Visual Studio 准备好显示监视表达式的值时，它会调用 [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)，后者又会调用 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)。 此过程将生成一个 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 对象，该对象包含表达式的值和类型。

在的此实现中 `IDebugParsedExpression::EvaluateSync` ，将同时分析和计算表达式。 此实现执行以下任务：

1. 分析并计算表达式，以生成保存值及其类型的泛型对象。 在 c # 中，这在 `object` c + + 中表示为，这表示为 `VARIANT` 。

2. 实例化 `CValueProperty` 在此示例中调用的类 () 实现 `IDebugProperty2` 接口，并将要返回的值存储在类中。

3. `IDebugProperty2`从对象返回接口 `CValueProperty` 。

## <a name="managed-code"></a>托管代码
这是 `IDebugParsedExpression::EvaluateSync` 托管代码中的的实现。 Helper 方法将 `Tokenize` 表达式分析为分析树。 Helper 函数 `EvalToken` 将该标记转换为一个值。 Helper 函数 `FindTerm` 以递归方式遍历分析树， `EvalToken` 为每个表示值的节点调用，并在表达式中 (加法或减法) 应用任何操作。

```csharp
namespace EEMC
{
    public class CParsedExpression : IDebugParsedExpression
    {
        public HRESULT EvaluateSync(
            uint evalFlags,
            uint timeout,
            IDebugSymbolProvider provider,
            IDebugAddress address,
            IDebugBinder binder,
            string resultType,
            out IDebugProperty2 result)
        {
            HRESULT retval = COM.S_OK;
            this.evalFlags = evalFlags;
            this.timeout = timeout;
            this.provider = provider;
            this.address = address;
            this.binder = binder;
            this.resultType = resultType;

            try
            {
                IDebugField field = null;
                // Tokenize, then parse.
                tokens = Tokenize(expression);
                result = new CValueProperty(
                        expression,
                        (int) FindTerm(EvalToken(tokens[0], out field),1),
                        field,
                        binder);
            }
            catch (ParseException)
            {
                result = new CValueProperty(expression, "Huh?");
                retval = COM.E_INVALIDARG;
            }
            return retval;
        }
    }
}
```

## <a name="unmanaged-code"></a>非托管代码
这是 `IDebugParsedExpression::EvaluateSync` 在非托管代码中实现的。 Helper 函数 `Evaluate` 分析和计算表达式，并返回 `VARIANT` 包含结果值的。 Helper 函数将 `VariantValueToProperty` 绑定 `VARIANT` 到 `CValueProperty` 对象。

```cpp
STDMETHODIMP CParsedExpression::EvaluateSync(
    in  DWORD                 evalFlags,
    in  DWORD                 dwTimeout,
    in  IDebugSymbolProvider* pprovider,
    in  IDebugAddress*        paddress,
    in  IDebugBinder*         pbinder,
    in  BSTR                  bstrResultType,
    out IDebugProperty2**     ppproperty )
{
    // dwTimeout parameter is ignored in this implementation.
    if (pprovider == NULL)
        return E_INVALIDARG;

    if (paddress == NULL)
        return E_INVALIDARG;

    if (pbinder == NULL)
        return E_INVALIDARG;

    if (ppproperty == NULL)
        return E_INVALIDARG;
    else
        *ppproperty = 0;

    HRESULT hr;
    VARIANT value;
    BSTR    bstrErrorMessage = NULL;
    hr = ::Evaluate( pprovider,
                     paddress,
                     pbinder,
                     m_expr,
                     &bstrErrorMessage,
                     &value );
    if (hr != S_OK)
    {
        if (bstrErrorMessage == NULL)
            return hr;

        //we can display better messages ourselves.
        HRESULT hrLocal = S_OK;
        VARIANT varType;
        VARIANT varErrorMessage;

        VariantInit( &varType );
        VariantInit( &varErrorMessage );
        varErrorMessage.vt      = VT_BSTR;
        varErrorMessage.bstrVal = bstrErrorMessage;

        CValueProperty* valueProperty = new CValueProperty();
        if (valueProperty != NULL)
        {
            hrLocal = valueProperty->Init(m_expr, varType, varErrorMessage);
            if (SUCCEEDED(hrLocal))
            {
                hrLocal = valueProperty->QueryInterface( IID_IDebugProperty2,
                        reinterpret_cast<void**>(ppproperty) );
            }
        }

        VariantClear(&varType);
        VariantClear(&varErrorMessage); //frees BSTR
        if (!valueProperty)
            return hr;
        valueProperty->Release();
        if (FAILED(hrLocal))
            return hr;
    }
    else
    {
        if (bstrErrorMessage != NULL)
            SysFreeString(bstrErrorMessage);

        hr = VariantValueToProperty( pprovider,
                                     paddress,
                                     pbinder,
                                     m_radix,
                                     m_expr,
                                     value,
                                     ppproperty );
        VariantClear(&value);
        if (FAILED(hr))
            return hr;
    }

    return S_OK;
}
```

## <a name="see-also"></a>请参阅
- [计算监视窗口表达式](../../extensibility/debugger/evaluating-a-watch-window-expression.md)
- [表达式计算的示例实现](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md)
