---
title: 计算监视表达式 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, watch expressions
- watch expressions
ms.assetid: 8317cd52-6fea-4e8f-a739-774dc06bd44b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d50abb359095a727b56bf40ab0d2c7ab1155d0c6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66315543"
---
# <a name="evaluate-a-watch-expression"></a>计算监视表达式
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

当 Visual Studio 已准备好显示监视表达式的值时，它将调用[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)，从而又会调用[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)。 此过程将生成[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)对象，其中包含的值和表达式的类型。

在此实现中的`IDebugParsedExpression::EvaluateSync`，该表达式进行分析和计算在同一时间。 此实现将执行以下任务：

1. 分析和计算表达式来生成用于保存的值，其类型的泛型对象。 在C#，这表示为`object`中时，在C++，这表示为`VARIANT`。

2. 实例化一个类 (称为`CValueProperty`在此示例中)，它实现`IDebugProperty2`接口，并存储在类中要返回的值。

3. 返回`IDebugProperty2`接口从`CValueProperty`对象。

## <a name="managed-code"></a>托管代码
这是一个实现的`IDebugParsedExpression::EvaluateSync`在托管代码中。 帮助器方法`Tokenize`分析到分析树的表达式。 帮助器函数`EvalToken`将令牌转换为一个值。 帮助器函数`FindTerm`以递归方式遍历分析树中，调用`EvalToken`表示值和表达式中应用任何操作 （加或减） 每个节点。

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

## <a name="unmanaged-code"></a>非托管的代码
这是一个实现的`IDebugParsedExpression::EvaluateSync`非托管代码中。 帮助器函数`Evaluate`分析和计算表达式，返回`VARIANT`保存生成的值。 帮助器函数`VariantValueToProperty`捆绑`VARIANT`到`CValueProperty`对象。

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
- [评估监视窗口表达式](../../extensibility/debugger/evaluating-a-watch-window-expression.md)
- [表达式计算的实现示例](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md)
