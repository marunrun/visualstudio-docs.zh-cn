---
title: IDebugComPlus符号提供程序2：：功能哈斯林信息 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- FunctionHasLineInfo
- IDebugComPlusSymbolProvider2::FunctionHasLineInfo
ms.assetid: e1b508f1-6521-492f-b110-ab957744a037
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3a574766b884bf1aeed253754534fee66967e9ef
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733457"
---
# <a name="idebugcomplussymbolprovider2functionhaslineinfo"></a>IDebugComPlusSymbolProvider2::FunctionHasLineInfo
确定指定方法是否具有行信息。

## <a name="syntax"></a>语法

```cpp
HRESULT FunctionHasLineInfo(
    IDebugAddress* pAddress
);
```

```csharp
int FunctionHasLineInfo(
    IDebugAddress pAddress
);
```

## <a name="parameters"></a>参数
`pAddress`\
[在]由[IDebugAddress 接口](../../../extensibility/debugger/reference/idebugaddress.md)表示的调试地址。 此地址必须是METHOD_ADDRESS。

## <a name="return-value"></a>返回值
如果成功，返回`S_OK`;否则，返回`S_FALSE`。

## <a name="example"></a>示例
下面的示例演示如何为公开[IDebugComPlusSymbolProvider2](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)接口的**CDebugSymbol提供程序**对象实现此方法。

```cpp
HRESULT CDebugSymbolProvider::FunctionHasLineInfo(
    IDebugAddress* pAddress
)
{
    HRESULT hr = S_OK;
    CDEBUG_ADDRESS address;
    CComPtr<CModule> pModule;

    METHOD_ENTRY( CDebugSymbolProvider::LoadSymbol );

    IfFalseGo( pAddress, E_INVALIDARG );

    IfFailGo( pAddress->GetAddress( &address ) );

    ASSERT(address.addr.dwKind == ADDRESS_KIND_METADATA_METHOD);
    IfFalseGo( address.addr.dwKind == ADDRESS_KIND_METADATA_METHOD, S_FALSE );

    IfFailGo( GetModule( address.GetModule(), &pModule) );

    if (!pModule->FunctionHasLineInfo( address.addr.addr.addrMethod.tokMethod,
                                       address.addr.addr.addrMethod.dwVersion))
    {

        // S_FALSE indicates this method does not have line info

        hr = S_FALSE;
    }

Error:

    METHOD_EXIT( CDebugSymbolProvider::LoadSymbol, hr );

    return hr;
}
```

## <a name="see-also"></a>请参阅
- [IDebugComPlusSymbolProvider2](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)
