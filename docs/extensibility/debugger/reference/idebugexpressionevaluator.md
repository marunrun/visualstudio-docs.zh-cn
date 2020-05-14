---
title: IDebug表达式评估器 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729384"
---
# <a name="idebugexpressionevaluator"></a>IDebugExpressionEvaluator
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

此接口表示表达式赋值器。

## <a name="syntax"></a>语法

```
IDebugExpressionEvaluator : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
表达式赋值器必须实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
要获取此接口，请使用赋值器的类 ID （CLSID） 通过`CoCreateInstance`方法实例化表达式赋值器。 请参阅示例。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示了 的方法`IDebugExpressionEvaluator`。

|方法|描述|
|------------|-----------------|
|[解析](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)|将表达式字符串转换为解析的表达式。|
|[GetMethodProperty](../../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)|获取方法的局部变量、参数和其他属性。|
|[GetMethodLocationProperty](../../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodlocationproperty.md)|将方法位置和偏移转换为内存地址。|
|[设置区域设置](../../../extensibility/debugger/reference/idebugexpressionevaluator-setlocale.md)|确定使用哪种语言来创建可打印的结果。|
|[SetRegistryRoot](../../../extensibility/debugger/reference/idebugexpressionevaluator-setregistryroot.md)|设置注册表根。 用于并行调试。|

## <a name="remarks"></a>备注
在典型情况下，调试引擎 （DE） 实例化表达式赋值器 （EE） 作为调用[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)的结果。 由于 DE 知道要使用的 EE 的语言和供应商，因此 DE 从注册表中获取 EE 的 CLSID（[用于调试功能的 SDK 帮助器](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)，`GetEEMetric`可帮助进行此检索）。

实例化 EE 后，DE 调用[Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)来解析表达式并将其存储在[IDebugParsed 表达式](../../../extensibility/debugger/reference/idebugparsedexpression.md)对象中。 稍后，对[评估同步](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)的调用将计算表达式。

## <a name="requirements"></a>要求
标题： ee.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="example"></a>示例
此示例演示如何实例化在源代码中给定符号提供程序和地址的表达式赋值器。 本示例使用用于调试库`GetEEMetric`的[SDK 帮助器](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)的函数 dbgmetric.lib。

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

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [用于调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
