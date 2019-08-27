---
title: IDebugExpressionEvaluator | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator
helpviewer_keywords:
- IDebugExpressionEvaluator interface
ms.assetid: 0636d8c3-625a-49fa-94b6-516f22b7e1bc
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ceffebf10838fe147475dcda54b385b844676de4
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63426463"
---
# <a name="idebugexpressionevaluator"></a>IDebugExpressionEvaluator
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 此接口表示表达式计算器。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugExpressionEvaluator : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 表达式计算器必须实现此接口。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 若要获取此接口，请实例化表达式计算器通过`CoCreateInstance`方法通过使用该计算器的类 ID (CLSID)。 请参阅示例。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugExpressionEvaluator`。  
  
|方法|描述|  
|------------|-----------------|  
|[分析](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)|将一个表达式字符串转换为已分析的表达式。|  
|[GetMethodProperty](../../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)|获取本地变量、 参数以及方法的其他属性。|  
|[GetMethodLocationProperty](../../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodlocationproperty.md)|方法的位置和偏移量转换为内存地址。|  
|[SetLocale](../../../extensibility/debugger/reference/idebugexpressionevaluator-setlocale.md)|确定要用于创建可打印结果的语言。|  
|[SetRegistryRoot](../../../extensibility/debugger/reference/idebugexpressionevaluator-setregistryroot.md)|设置的注册表根目录。 用于通过并行调试。|  
  
## <a name="remarks"></a>备注  
 在典型的情况下，调试引擎 (DE) 会实例化表达式计算器 (EE) 调用[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)。 DE DE 获知的语言和 EE 它想要使用的供应商，因为从注册表获取 EE 的 CLSID ([以便进行调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)函数， `GetEEMetric`，可以帮助完成此检索)。  
  
 EE 实例化后，调用 DE[分析](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)分析表达式并将其存储在[IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)对象。 更高版本，调用[EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)计算表达式的值。  
  
## <a name="requirements"></a>要求  
 标头： ee.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="example"></a>示例  
 此示例演示如何实例化表达式计算器中的源代码中给定符号提供程序和地址。 此示例使用一个函数`GetEEMetric`，从[以便进行调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)库、 dbgmetric.lib。  
  
```cpp#  
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
            CLSID clsidEE      = { 0 };  
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
 [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)   
 [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)   
 [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)   
 [用于调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
