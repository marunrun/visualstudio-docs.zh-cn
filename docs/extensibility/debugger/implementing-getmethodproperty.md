---
title: 实现 GetMethodProperty |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- GetMethodProperty method
- IDebugExpressionEvaluator2 property
ms.assetid: 6305874f-a2c4-4432-834c-07530ea84bff
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f802733f74677a0426a99fb662302d816ad34721
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66344296"
---
# <a name="implement-getmethodproperty"></a>实现 GetMethodProperty
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

Visual Studio 会调用调试引擎 (DE) [GetDebugProperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)，从而又会调用[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)来获取有关当前方法的堆栈帧上的信息。

此实现`IDebugExpressionEvaluator::GetMethodProperty`执行下列任务：

1. 调用[GetContainerField](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)，并传入[IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)对象。 符号提供程序 (SP) 将返回[IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md)表示包含指定的地址的方法。

2. 获取[IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md)从`IDebugContainerField`。

3. 实例化一个类 (称为`CFieldProperty`在此示例中)，它实现[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)接口并包含`IDebugMethodField`SP 从返回的对象

4. 返回`IDebugProperty2`接口从`CFieldProperty`对象。

## <a name="managed-code"></a>托管代码
此示例演示一种实现`IDebugExpressionEvaluator::GetMethodProperty`在托管代码中。

```csharp
namespace EEMC
{
    [GuidAttribute("462D4A3D-B257-4AEE-97CD-5918C7531757")]
    public class EEMCClass : IDebugExpressionEvaluator
    {
        public HRESULT GetMethodProperty(
                IDebugSymbolProvider symbolProvider,
                IDebugAddress        address,
                IDebugBinder         binder,
                int                  includeHiddenLocals,
            out IDebugProperty2      property)
        {
            IDebugContainerField containerField = null;
            IDebugMethodField methodField       = null;
            property = null;

            // Get the containing method field.
            symbolProvider.GetContainerField(address, out containerField);
            methodField = (IDebugMethodField) containerField;

            // Return the property of method field.
            property = new CFieldProperty(symbolProvider, address, binder, methodField);
            return COM.S_OK;
        }
    }
}
```

## <a name="unmanaged-code"></a>非托管的代码
此示例演示一种实现`IDebugExpressionEvaluator::GetMethodProperty`非托管代码中。

```
[CPP]
STDMETHODIMP CExpressionEvaluator::GetMethodProperty(
        in IDebugSymbolProvider *pprovider,
        in IDebugAddress        *paddress,
        in IDebugBinder         *pbinder,
        in BOOL                  includeHiddenLocals,
        out IDebugProperty2    **ppproperty
    )
{
    if (pprovider == NULL)
        return E_INVALIDARG;

    if (ppproperty == NULL)
        return E_INVALIDARG;
    else
        *ppproperty = 0;

    HRESULT hr;
    IDebugContainerField* pcontainer = NULL;

    hr = pprovider->GetContainerField(paddress, &pcontainer);
    if (FAILED(hr))
        return hr;

    IDebugMethodField*    pmethod    = NULL;
    hr = pcontainer->QueryInterface( IID_IDebugMethodField,
            reinterpret_cast<void**>(&pmethod));
    pcontainer->Release();
    if (FAILED(hr))
        return hr;

    CFieldProperty* pfieldProperty = new CFieldProperty( pprovider,
                                                         paddress,
                                                         pbinder,
                                                         pmethod );
    pmethod->Release();
    if (!pfieldProperty)
        return E_OUTOFMEMORY;

    hr = pfieldProperty->Init();
    if (FAILED(hr))
    {
        pfieldProperty->Release();
        return hr;
    }

    hr = pfieldProperty->QueryInterface( IID_IDebugProperty2,
            reinterpret_cast<void**>(ppproperty));
    pfieldProperty->Release();

    return hr;
}
```

## <a name="see-also"></a>请参阅
- [局部的实现示例](../../extensibility/debugger/sample-implementation-of-locals.md)
