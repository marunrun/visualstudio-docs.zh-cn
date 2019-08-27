---
title: IDebugSymbolProvider | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider
helpviewer_keywords:
- IDebugSymbolProvider interface
ms.assetid: df5f095f-1dee-46f9-84cf-92417c71d5fb
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b760b106992b200576258ab6becb1ae3849b8f3a
ms.sourcegitcommit: da4079f5b6ec884baf3108cbd0519d20cb64c70b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62420922"
---
# <a name="idebugsymbolprovider"></a>IDebugSymbolProvider
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示的符号提供程序提供了符号和类型，返回为字段。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugSymbolProvider : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 符号提供程序必须实现此接口可提供符号和类型的表达式计算器的信息。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 此接口通过使用 COM 的`CoCreateInstance`（适用于非托管的符号提供程序） 的函数或通过加载相应托管代码程序集和实例化符号提供程序根据在该程序集中找到的信息。 调试引擎实例化才能与表达式计算器结合使用的符号提供程序。 请参阅实例化此接口的一种方法的示例。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugSymbolProvider`。  
  
|方法|描述|  
|------------|-----------------|  
|`Initialize`|已否决。 请勿使用。|  
|`Uninitialize`|已否决。 请勿使用。|  
|[GetContainerField](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)|获取包含调试地址的字段。|  
|`GetField`|已否决。 请勿使用。|  
|[GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)|将映射到一个数组的调试地址的文档位置。|  
|[GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)|将文档上下文映射到调试地址的数组。|  
|[GetContextFromAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontextfromaddress.md)|将调试地址映射到文档上下文。|  
|[GetLanguage](../../../extensibility/debugger/reference/idebugsymbolprovider-getlanguage.md)|获取用于编译调试地址处的代码的语言。|  
|`GetGlobalContainer`|已否决。 请勿使用。|  
|[GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md)|获取表示完全限定的方法名称的字段。|  
|[GetClassTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md)|获取表示完全限定的类名的类字段类型。|  
|[GetNamespacesUsedAtAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)|创建命名空间与调试地址相关联的枚举器。|  
|[GetTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-gettypebyname.md)|将符号名称映射到符号类型。|  
|[GetNextAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnextaddress.md)|获取遵循一种方法中的给定的调试地址的调试地址。|  
  
## <a name="remarks"></a>备注  
 此接口映射文档位置到调试地址，反之亦然。  
  
## <a name="requirements"></a>要求  
 标头： sh.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="example"></a>示例  
 此示例演示如何实例化符号提供程序，提供它的 GUID （调试引擎必须知道此值）。  
  
```cpp#  
// A debug engine uses its own symbol provider and would know the GUID  
// of that provider.  
IDebugSymbolProvider *GetSymbolProvider(GUID *pSymbolProviderGuid)  
{  
    // This is typically defined globally.  For this example, it is  
    // defined here.  
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";  
    IDebugSymbolProvider *pProvider = NULL;  
    if (pSymbolProviderGuid != NULL) {  
        CLSID clsidProvider = { 0 };  
        ::GetSPMetric(*pSymbolProviderGuid,  
                      storetypeFile,  
                      metricCLSID,  
                      &clsidProvider,  
                      strRegistrationRoot);  
        if (IsEqualGUID(clsidProvider,GUID_NULL)) {  
            // No file type provider, try metadata provider.  
            ::GetSPMetric(*pSymbolProviderGuid,  
                          ::storetypeMetadata,  
                          metricCLSID,  
                          &clsidProvider,  
                          strRegistrationRoot);  
        }  
        if (!IsEqualGUID(clsidProvider,GUID_NULL)) {  
            CComPtr<IDebugSymbolProvider> spSymbolProvider;  
            spSymbolProvider.CoCreateInstance(clsidProvider);  
            if (spSymbolProvider != NULL) {  
                pProvider = spSymbolProvider.Detach();  
            }  
        }  
    }  
    return(pProvider);  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
