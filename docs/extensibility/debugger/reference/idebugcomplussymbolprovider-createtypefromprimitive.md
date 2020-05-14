---
title: IDebugcomPlus符号提供程序：：从原始创建类型 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::CreateTypeFromPrimitive
- CreateTypeFromPrimitive
ms.assetid: 37213cc2-a038-42ea-9b28-3ae40d4cfe69
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5b5759110c60bf25c0197c370bebdd45f71c2a22
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734154"
---
# <a name="idebugcomplussymbolprovidercreatetypefromprimitive"></a>IDebugComPlusSymbolProvider::CreateTypeFromPrimitive
从指定的基元类型创建类型。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateTypeFromPrimitive(
    DWORD          dwPrimType,
    IDebugAddress* pAddress,
    IDebugField**  ppType
);
```

```csharp
int CreateTypeFromPrimitive(
    uint          dwPrimType,
    IDebugAddress pAddress,
    IDebugField   ppType
);
```

## <a name="parameters"></a>参数
`dwPrimType`\
[在]表示基元[类型的 CorElementType 枚举中](/dotnet/framework/unmanaged-api/metadata/corelementtype-enumeration)的值。

`pAddress`\
[在]由[IDebug 地址](../../../extensibility/debugger/reference/idebugaddress.md)接口表示的地址对象。

`ppType`\
[在]返回描述该类型的[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象。

## <a name="return-value"></a>返回值
如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="example"></a>示例
下面的示例演示如何为公开[IDebugComPlusSymbol提供程序](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)接口的**CDebugSymbol提供程序**对象实现此方法。

```cpp
HRESULT CDebugSymbolProvider::CreateTypeFromPrimitive(
    DWORD dwPrimType,
    IDebugAddress* pAddress,
    IDebugField** ppType)
{
    HRESULT hr = S_OK;
    CDEBUG_ADDRESS addr;
    const COR_SIGNATURE* pTypeInfo = (const COR_SIGNATURE*) & dwPrimType;
    CDebugGenericParamScope* pGenScope = NULL;

    //
    // This function will only work for primitive types
    //

    METHOD_ENTRY( CDebugSymbolProvider::CreateTypeFromPrimitive );

    IfFailGo( pAddress->GetAddress( &addr ) );

    IfNullGo( pGenScope = new CDebugGenericParamScope(addr.GetModule(), addr.tokClass, addr.GetMethod()), E_OUTOFMEMORY );

    IfFailGo( CreateType( pTypeInfo,
                          1,
                          addr.GetModule(),
                          addr.GetMethod(),
                          pGenScope,
                          ppType ) );

    METHOD_EXIT( CDebugSymbolProvider::CreateTypeFromPrimitive, hr );

Error:

    RELEASE( pGenScope );
    return hr;
}
```

## <a name="see-also"></a>请参阅
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
