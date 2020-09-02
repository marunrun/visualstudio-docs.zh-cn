---
title: IDebugExpressionEvaluator |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator
helpviewer_keywords:
- IDebugExpressionEvaluator interface
ms.assetid: 0636d8c3-625a-49fa-94b6-516f22b7e1bc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7e8dd910e4edc110abb40dde14b4cb85ff54a70a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80729384"
---
# <a name="idebugexpressionevaluator"></a>IDebugExpressionEvaluator
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

此接口表示表达式计算器。

## <a name="syntax"></a>语法

```
IDebugExpressionEvaluator : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
表达式计算器必须实现此接口。

## <a name="notes-for-callers"></a>调用方说明
若要获取此接口，请通过 `CoCreateInstance` 使用 ID (CLSID) 的类 ID 来实例化该方法的表达式计算器。 请参阅示例。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示的方法 `IDebugExpressionEvaluator` 。

|方法|说明|
|------------|-----------------|
|Parse|将表达式字符串转换为分析的表达式。|
|[GetMethodProperty](../../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)|获取方法的局部变量、参数和其他属性。|
|[GetMethodLocationProperty](../../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodlocationproperty.md)|将方法位置和偏移量转换为内存地址。|
|[SetLocale](../../../extensibility/debugger/reference/idebugexpressionevaluator-setlocale.md)|确定要使用哪种语言创建可打印结果。|
|[SetRegistryRoot](../../../extensibility/debugger/reference/idebugexpressionevaluator-setregistryroot.md)|设置注册表根。 用于并行调试。|

## <a name="remarks"></a>备注
在典型情况下，调试引擎 (DE) 实例化表达式计算器 (EE) 作为调用 [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)的结果。 由于 DE 知道了它想要使用的 EE 的语言和供应商，因此，从注册表中获取了用于调试函数的 " [SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) " (的 EE CLSID， `GetEEMetric` 这有助于此检索) 。

在实例化 EE 后，DE 调用 [parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) 分析表达式，并将其存储在 [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md) 对象中。 稍后，对 [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) 的调用将计算表达式的值。

## <a name="requirements"></a>要求
标头： ee。h

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>示例
此示例演示如何在给定符号提供程序的情况下实例化表达式计算器，并在源代码中实例化地址。 此示例使用 `GetEEMetric` [SDK 帮助程序中调试](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) 库 dbgmetric 的函数。

```cpp
IDebugExpressionEvaluator GetExpressionEvaluator(IDebugSymbolProvider pSymbolProvider,
                                                 IDebugAddress *pSourceAddress)
{
    // This is typically defined globally but is specified here just
    // for this example.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";

    IDebugExpressionEvaluator *pEE = NULL;
    if (pSymbolProvider != NULL && pSourceAddress != NULL) {
        HRESULT hr         = S_OK;
        GUID  languageGuid = { 0 };
        GUID  vendorGuid   = { 0 };

        hr = pSymbolProvider->GetLanguage(pSourceAddress,
                                          &languageGuid,
                                          &vendorGuid);
        if (SUCCEEDED(hr)) {
            CLSID clsidEE = { 0 };
            CComPtr<IDebugExpressionEvaluator> spExpressionEvaluator;
            // Get the expression evaluator's CLSID from the registry.
            ::GetEEMetric(languageGuid,
                          vendorGuid,
                          metricCLSID,
                          &clsidEE,
                          strRegistrationRoot);
            if (!IsEqualGUID(clsidEE,GUID_NULL)) {
                // Instantiate the expression evaluator.
                spExpressionEvaluator.CoCreateInstance(clsidEE);
            }
            if (spExpressionEvaluator != NULL) {
                pEE = spExpressionEvaluator.Detach();
            }
        }
    }
    return pEE;
}
```

## <a name="see-also"></a>另请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [用于调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
