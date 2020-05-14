---
title: IDebug符号提供程序 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider
helpviewer_keywords:
- IDebugSymbolProvider interface
ms.assetid: df5f095f-1dee-46f9-84cf-92417c71d5fb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 11e180288a9312d9af5a3d3b1bd63d8f2266f581
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719168"
---
# <a name="idebugsymbolprovider"></a>IDebugSymbolProvider
此接口表示提供符号和类型的符号提供程序，将它们作为字段返回。

## <a name="syntax"></a>语法

```
IDebugSymbolProvider : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
符号提供程序必须实现此接口，以便向表达式赋值器提供符号和键入信息。

## <a name="notes-for-callers"></a>呼叫者备注
此接口是通过使用 COM 的功能`CoCreateInstance`（对于非托管符号提供程序）或通过加载适当的托管代码程序集并根据该程序集中的信息实例化符号提供程序获得的。 调试引擎实例化符号提供程序与表达式赋值器协调工作。 有关实例化此接口的一种方法，请参阅示例。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示了 的方法`IDebugSymbolProvider`。

|方法|描述|
|------------|-----------------|
|`Initialize`|已弃用。 请勿使用。|
|`Uninitialize`|已弃用。 请勿使用。|
|[GetContainerField](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)|获取包含调试地址的字段。|
|`GetField`|已弃用。 请勿使用。|
|[GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)|将文档位置映射到调试地址数组中。|
|[GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)|将文档上下文映射到调试地址数组中。|
|[GetContextFromAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontextfromaddress.md)|将调试地址映射到文档上下文。|
|[GetLanguage](../../../extensibility/debugger/reference/idebugsymbolprovider-getlanguage.md)|获取用于在调试地址编译代码的语言。|
|`GetGlobalContainer`|已弃用。 请勿使用。|
|[GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md)|获取表示完全限定方法名称的字段。|
|[GetClassTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md)|获取表示完全限定类名称的类字段类型。|
|[GetNamespacesUsedAtAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)|为与调试地址关联的命名空间创建枚举器。|
|[GetTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-gettypebyname.md)|将符号名称映射到符号类型。|
|[GetNextAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnextaddress.md)|获取方法中给定调试地址后面的调试地址。|

## <a name="remarks"></a>备注
此接口将文档位置映射到调试地址，反之亦然。

## <a name="requirements"></a>要求
标题： sh.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="example"></a>示例
此示例演示如何实例化符号提供程序（给定其 GUID（调试引擎必须知道此值）。

```cpp
// A debug engine uses its own symbol provider and would know the GUID
// of that provider.
IDebugSymbolProvider *GetSymbolProvider(GUID *pSymbolProviderGuid)
{
    // This is typically defined globally. For this example, it is
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
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
