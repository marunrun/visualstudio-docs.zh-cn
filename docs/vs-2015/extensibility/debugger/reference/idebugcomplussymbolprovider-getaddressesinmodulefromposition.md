---
title: IDebugComPlusSymbolProvider：： GetAddressesInModuleFromPosition |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- GetAddressesInModuleFromPosition
- IDebugComPlusSymbolProvider::GetAddressesInModuleFromPosition
ms.assetid: f901c66e-f53c-4ea0-8004-d8fcbf46f916
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4471997a5497413869c3c4662592f4c585c2d76d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194828"
---
# <a name="idebugcomplussymbolprovidergetaddressesinmodulefromposition"></a>IDebugComPlusSymbolProvider::GetAddressesInModuleFromPosition
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

将指定模块中的文档位置映射到一个调试地址数组。  
  
## <a name="syntax"></a>语法  
  
```  
[C++]  
HRESULT GetAddressesInModuleFromPosition(  
   ULONG32                  ulAppDomainID,  
   GUID                     guidModule,  
   IDebugDocumentPosition2* pDocPos,  
   BOOL                     fStatmentOnly,  
   IEnumDebugAddresses**    ppEnumBegAddresses,  
   IEnumDebugAddresses**    ppEnumEndAddresses  
);  
```  
  
```  
[C#]  
int GetAddressesInModuleFromPosition(  
   uint                    ulAppDomainID,  
   Guid                    guidModule,  
   IDebugDocumentPosition2 pDocPos,  
   bool                    fStatmentOnly,  
   out IEnumDebugAddresses ppEnumBegAddresses,  
   out IEnumDebugAddresses ppEnumEndAddresses  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ulAppDomainID`  
 中应用程序域标识符。  
  
 `guidModule`  
 中模块的唯一标识符。  
  
 `pDocPos`  
 中文档位置。  
  
 `fStatmentOnly`  
 中如果 `TRUE` 为，则将调试地址限制为单个语句。  
  
 `ppEnumBegAddresses`  
 弄返回与此语句或行关联的起始调试地址的枚举数。  
  
 `ppEnumEndAddresses`  
 弄返回与此语句或行相关联的结束调试地址的枚举数。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="example"></a>示例  
 下面的示例演示如何为公开[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)接口的**CDebugSymbolProvider**对象实现此方法。  
  
```cpp#  
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
  
## <a name="see-also"></a>另请参阅  
 [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
