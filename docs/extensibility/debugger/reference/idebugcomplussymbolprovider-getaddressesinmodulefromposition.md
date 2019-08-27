---
title: IDebugComPlusSymbolProvider::GetAddressesInModuleFromPosition | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetAddressesInModuleFromPosition
- IDebugComPlusSymbolProvider::GetAddressesInModuleFromPosition
ms.assetid: f901c66e-f53c-4ea0-8004-d8fcbf46f916
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3000b93a9ce7f3ba56325943d48c5ac686ddde38
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66338715"
---
# <a name="idebugcomplussymbolprovidergetaddressesinmodulefromposition"></a>IDebugComPlusSymbolProvider::GetAddressesInModuleFromPosition
将指定的模块中的文档位置映射到调试地址的数组。

## <a name="syntax"></a>语法

```cpp
HRESULT GetAddressesInModuleFromPosition(
   ULONG32                  ulAppDomainID,
   GUID                     guidModule,
   IDebugDocumentPosition2* pDocPos,
   BOOL                     fStatmentOnly,
   IEnumDebugAddresses**    ppEnumBegAddresses,
   IEnumDebugAddresses**    ppEnumEndAddresses
);
```

```csharp
int GetAddressesInModuleFromPosition(
   uint                    ulAppDomainID,
   Guid                    guidModule,
   IDebugDocumentPosition2 pDocPos,
   bool                    fStatmentOnly,
   out IEnumDebugAddresses ppEnumBegAddresses,
   out IEnumDebugAddresses ppEnumEndAddresses
);
```

## <a name="parameters"></a>参数
`ulAppDomainID`\
[in]应用程序域标识符。

`guidModule`\
[in]该模块的唯一标识符。

`pDocPos`\
[in]文档位置中。

`fStatmentOnly`\
[in]如果`TRUE`，限制到单个语句的调试地址。

`ppEnumBegAddresses`\
[out]返回与此语句或行相关联的起始调试地址的枚举器。

`ppEnumEndAddresses`\
[out]返回与此语句或行的结束调试地址的枚举器。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="example"></a>示例
 下面的示例演示如何实现此方法对于**CDebugSymbolProvider**对象，它公开[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)接口。

```cpp
HRESULT CDebugSymbolProvider::GetAddressesInModuleFromPosition(
    ULONG32 ulAppDomainID,
    GUID guidModule,
    IDebugDocumentPosition2* pDocPos,
    BOOL fStatementOnly,
    IEnumDebugAddresses** ppEnumBegAddresses,
    IEnumDebugAddresses** ppEnumEndAddresses
)
{
    GUID guidNULL = {0};

    if (guidNULL == guidModule)
    {
        return GetAddressesInAppDomainFromPosition( ulAppDomainID,
                pDocPos,
                fStatementOnly,
                ppEnumBegAddresses,
                ppEnumEndAddresses );
    }
    else
    {
        return GetAddressesInModuleFromPositionHelper( ulAppDomainID,
                guidModule,
                pDocPos,
                fStatementOnly,
                ppEnumBegAddresses,
                ppEnumEndAddresses );
    }
}

HRESULT CDebugSymbolProvider::GetAddressesInModuleFromPositionHelper(
    ULONG32 ulAppDomainID,
    GUID guidModule,
    IDebugDocumentPosition2* pDocPos,
    BOOL fStatementOnly,
    IEnumDebugAddresses** ppEnumBegAddresses,
    IEnumDebugAddresses** ppEnumEndAddresses
)
{
    HRESULT hr = S_OK;
    CComBSTR bstrFileName;
    TEXT_POSITION posBeg;
    TEXT_POSITION posEnd;
    DWORD dwLine;
    USHORT segRet = 0;
    ULONG offRet = 0;
    CAddrList listAddr;
    CAddrList listAddrEnd;
    CAddrList* plistAddrEnd = NULL;
    bool fFileFound = false;
    Module_ID idModule(ulAppDomainID, guidModule);
    DWORD dwListCount;
    bool fFoundAddresses = false;
    CComPtr<CModule> pmodule;
    DWORD dwBegCol = 0;
    DWORD dwEndCol = 0;

    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));
    ASSERT(IsValidInterfacePtr(pDocPos, IDebugDocumentPosition2));
    ASSERT(IsValidWritePtr(ppEnumBegAddresses, IEnumDebugAddresses*));

    METHOD_ENTRY(CDebugSymbolProvider::GetAddressesInModuleFromPositionHelper);

    // Bail on Invalid Args

    IfFalseGo( pDocPos && ppEnumBegAddresses, E_INVALIDARG );

    *ppEnumBegAddresses = NULL;
    if (ppEnumEndAddresses)
    {
        *ppEnumEndAddresses = NULL;
        plistAddrEnd = &listAddrEnd;
    }

    // Get the Position

    IfFailGo( pDocPos->GetFileName(&bstrFileName) );
    IfFailGo( pDocPos->GetRange(&posBeg, &posEnd) );

    // Iterate over the module list accumulating addresses
    // that match the position

    dwLine = posBeg.dwLine;
    IfFailGo( GetModule( idModule, &pmodule ) );
    dwListCount = listAddr.GetCount();

    if ( fStatementOnly )
    {
        dwBegCol = posBeg.dwColumn;
        dwEndCol = posBeg.dwLine == posEnd.dwLine ? posEnd.dwColumn : DWORD( -1);
    }
    else
    {
        dwBegCol = 0;
        dwEndCol = DWORD( -1);
    }

    while (!fFoundAddresses && dwLine <= posEnd.dwLine )
    {
        hr = pmodule->GetAddressesFromLine( bstrFileName,
                                            dwLine,
                                            posEnd.dwLine,
                                            dwBegCol,
                                            dwEndCol,
                                            &listAddr,
                                            plistAddrEnd );

        dwLine++;
        dwBegCol = 0;
        dwEndCol = dwLine == posEnd.dwLine ? posEnd.dwColumn : DWORD( -1);

        if (hr == E_SH_INVALID_POSITION)
        {
            fFileFound = true;
            break;
        }

        if (FAILED(hr))
        {
            // Move on to the next module
            break;
        }

        fFileFound = true;
        fFoundAddresses = listAddr.GetCount() != dwListCount;
    }

    // Distinguish no file from bad position in the file
    IfFalseGo( fFileFound, E_SH_FILE_NOT_FOUND);

    // If the list is empty the position is bad
    IfFalseGo( listAddr.GetCount(), E_SH_INVALID_POSITION );

    // Create enumerators
    IfFailGo( CreateEnumerator( ppEnumBegAddresses, &listAddr ) );
    if (ppEnumEndAddresses)
    {
        IfFailGo( CreateEnumerator( ppEnumEndAddresses, &listAddrEnd ) );
    }

Error:

    METHOD_EXIT(CDebugSymbolProvider::GetAddressesInModuleFromPositionHelper, hr);

    return hr;
}
```

## <a name="see-also"></a>请参阅
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)