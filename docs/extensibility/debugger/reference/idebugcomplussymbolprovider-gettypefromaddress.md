---
title: IDebugComPlusSymbolProvider::GetTypeFromAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::GetTypeFromAddress
- GetTypeFromAddress
ms.assetid: 01f21ff9-e8a5-4e5f-9f7b-1b6de8b1432f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7cc1a0e5bb25edcbfae047a088c20884330e81ee
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66336705"
---
# <a name="idebugcomplussymbolprovidergettypefromaddress"></a>IDebugComPlusSymbolProvider::GetTypeFromAddress
检索到给出其调试地址符号类型。

## <a name="syntax"></a>语法

```cpp
HRESULT GetTypeFromAddress(
    IDebugAddress* pAddress,
    IDebugField**  ppField
);
```

```csharp
int GetTypeFromAddress(
    IDebugAddress   pAddress,
    out IDebugField ppField
);
```

## <a name="parameters"></a>参数
`pAddress`\
[in]由表示的调试地址[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)接口。

`ppField`\
[out]返回数组类型，它是由[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)接口。

## <a name="return-value"></a>返回值
如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="example"></a>示例
下面的示例演示如何实现此方法对于**CDebugSymbolProvider**对象，它公开[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)接口。

```cpp
HRESULT CDebugSymbolProvider::GetTypeFromAddress(
    IDebugAddress *pAddress,
    IDebugField **ppField)
{
    HRESULT hr = E_FAIL;
    CDEBUG_ADDRESS da;
    CDebugGenericParamScope* pGenScope = NULL;

    METHOD_ENTRY( CDebugDynamicFieldSymbol::GetTypeFromPrimitive );

    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));
    ASSERT(IsValidWritePtr(ppField, IDebugField*));

    IfFailGo( pAddress->GetAddress(&da) );

    switch ( da.addr.dwKind )
    {
        case ADDRESS_KIND_METADATA_LOCAL:
        case ADDRESS_KIND_METADATA_PARAM:
        case ADDRESS_KIND_METADATA_FIELD:
        case ADDRESS_KIND_METADATA_ARRAYELEM:
        case ADDRESS_KIND_METADATA_METHOD:
            {
                IfFailGo( this->CreateClassType(da.GetModule(), da.tokClass, ppField) );
                break;
            }

        case ADDRESS_KIND_METADATA_RETVAL:
            {
                if ( da.addr.addr.addrRetVal.dwCorType )
                {

                    IfNullGo( pGenScope = new CDebugGenericParamScope(da.GetModule(), da.tokClass, da.GetMethod()), E_OUTOFMEMORY );
                    IfFailGo( this->CreateType((const COR_SIGNATURE*)(&da.addr.addr.addrRetVal.rgSig),
                                               da.addr.addr.addrRetVal.dwSigSize,
                                               da.GetModule(),
                                               mdMethodDefNil,
                                               pGenScope,
                                               ppField) );
                }
                else
                {
                    IfFailGo( this->CreateClassType(da.GetModule(), da.tokClass, ppField) );
                }

                break;
            }

        default:
            {
                ASSERT(!"Address type not supported.");
            }
    }

Error:

    METHOD_EXIT( CDebugDynamicFieldSymbol::GetTypeFromPrimitive, hr );

    RELEASE( pGenScope );

    return hr;
}
```

## <a name="see-also"></a>请参阅
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
