---
title: IDebugSymbolProvider |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62420922"
---
# <a name="idebugsymbolprovider"></a>IDebugSymbolProvider
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示一个符号提供程序，该提供程序提供符号和类型，并将它们作为字段返回。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugSymbolProvider : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 符号提供程序必须实现此接口，才能向表达式计算器提供符号和类型信息。  
  
## <a name="notes-for-callers"></a>调用方说明  
 此接口是通过以下方法获取的：使用 COM 的 `CoCreateInstance` 函数 (用于非托管符号提供程序) 或者加载相应的托管代码程序集，并根据该程序集中找到的信息来实例化符号提供程序。 调试引擎实例化符号提供程序，以便与表达式计算器协调工作。 有关实例化此接口的方法，请参阅示例。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDebugSymbolProvider` 。  
  
|方法|说明|  
|------------|-----------------|  
|`Initialize`|已否决。 请勿使用。|  
|`Uninitialize`|已否决。 请勿使用。|  
|[GetContainerField](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)|获取包含调试地址的字段。|  
|`GetField`|已否决。 请勿使用。|  
|[GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)|将文档位置映射到一个调试地址数组。|  
|[GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)|将文档上下文映射到一个调试地址数组。|  
|[GetContextFromAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontextfromaddress.md)|将调试地址映射到文档上下文。|  
|[GetLanguage](../../../extensibility/debugger/reference/idebugsymbolprovider-getlanguage.md)|获取用于在调试地址编译代码的语言。|  
|`GetGlobalContainer`|已否决。 请勿使用。|  
|[GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md)|获取表示完全限定方法名称的字段。|  
|[GetClassTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md)|获取表示完全限定类名的类字段类型。|  
|[GetNamespacesUsedAtAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)|创建与调试地址相关联的命名空间的枚举器。|  
|[GetTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-gettypebyname.md)|将符号名称映射到符号类型。|  
|[GetNextAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnextaddress.md)|获取在方法中跟随给定调试地址的调试地址。|  
  
## <a name="remarks"></a>备注  
 此接口将文档位置映射到调试地址中，反之亦然。  
  
## <a name="requirements"></a>要求  
 标头： sh。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="example"></a>示例  
 此示例演示如何实例化符号提供程序（给定其 GUID (调试引擎必须知道此值) 。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
