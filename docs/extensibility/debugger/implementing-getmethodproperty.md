---
title: 实现 GetMethodProperty |Microsoft Docs
description: 了解 Visual Studio 如何使用调试引擎的 GetDebugProperty 获取有关堆栈帧上的当前方法的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- GetMethodProperty method
- IDebugExpressionEvaluator2 property
ms.assetid: 6305874f-a2c4-4432-834c-07530ea84bff
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6028bd92611e7d5dc8a7e05fcf98bc360de7e9ed
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2020
ms.locfileid: "96559909"
---
# <a name="implement-getmethodproperty"></a>实现 GetMethodProperty
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

Visual Studio 将调用调试引擎 (DE) [GetDebugProperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)，后者又调用 [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) 来获取有关堆栈帧上的当前方法的信息。

此实现 `IDebugExpressionEvaluator::GetMethodProperty` 执行以下任务：

1. 调用 [GetContainerField](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)，传入 [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md) 对象。 符号提供程序 (SP) 返回表示包含指定地址的方法的 [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) 。

2. 从获取 [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) `IDebugContainerField` 。

3. 实例化 (`CFieldProperty` 在此示例中调用的类) 实现 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 接口并包含 `IDebugMethodField` 从 SP 返回的对象。

4. `IDebugProperty2`从对象返回接口 `CFieldProperty` 。

## <a name="managed-code"></a>托管代码
此示例演示如何 `IDebugExpressionEvaluator::GetMethodProperty` 在托管代码中实现。

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

## <a name="unmanaged-code"></a>非托管代码
此示例演示如何 `IDebugExpressionEvaluator::GetMethodProperty` 在非托管代码中实现。

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

## <a name="see-also"></a>另请参阅
- [局部变量的示例实现](../../extensibility/debugger/sample-implementation-of-locals.md)
