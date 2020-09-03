---
title: IDebugComPlusSymbolProvider：： GetNameFromToken |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::GetNameFromToken
- GetNameFromToken
ms.assetid: 6e8cf468-5fd1-4655-93ed-88828d6068b7
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 94cca3ebf25c86579ce601d614618ff431629af7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194689"
---
# <a name="idebugcomplussymbolprovidergetnamefromtoken"></a>IDebugComPlusSymbolProvider::GetNameFromToken
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

根据给定的元数据对象，返回与指定标记关联的名称。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetNameFromToken (  
   IUnknown* pMetadataImport,  
   DWORD     dwToken,  
   BSTR*     pbstrName  
);  
```  
  
```csharp  
int GetNameFromToken (  
   object     pMetadataImport,  
   uint       dwToken,  
   out string pbstrName  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pMetadataImport`  
 中包含元数据信息的对象。  
  
 `dwToken`  
 中要命名的标记。  
  
 `pbstrName`  
 弄对应于标记的名称。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="example"></a>示例  
 下面的示例演示如何为公开[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)接口的**CDebugSymbolProvider**对象实现此方法。  
  
```cpp#  
HRESULT CDebugSymbolProvider::GetNameFromToken(  
    IUnknown* pMetadataImport,  
    DWORD dwToken,  
    BSTR* pbstrName  
)  
{  
    HRESULT hr = S_OK;  
    CComPtr<IMetaDataImport> pMetaData;  
  
    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));  
    ASSERT(IsValidInterfacePtr(pMetadataImport, IUnknown));  
  
    METHOD_ENTRY(CDebugSymbolProvider::GetNameFromToken);  
  
    IfFalseGo( pMetadataImport && pbstrName, E_INVALIDARG );  
  
    *pbstrName = NULL;  
    IfFailGo( pMetadataImport->QueryInterface( IID_IMetaDataImport,  
              (void**) &pMetaData ) );  
  
    switch ( TypeFromToken(dwToken) )  
    {  
        case mdtModule:  
            IfFailGo( GetModuleName( pMetaData, dwToken, pbstrName) );  
            break;  
  
        case mdtTypeDef:  
            IfFailGo( GetTypeName( pMetaData, dwToken, pbstrName) );  
            break;  
  
        case mdtFieldDef:  
            IfFailGo( GetFieldName( pMetaData, dwToken, pbstrName) );  
            break;  
  
        case mdtMethodDef:  
            IfFailGo( GetMethodName( pMetaData, dwToken, pbstrName) );  
            break;  
  
        case mdtEvent:  
            IfFailGo( GetEventName( pMetaData, dwToken, pbstrName) );  
            break;  
  
        case mdtProperty:  
            IfFailGo( GetPropertyName( pMetaData, dwToken, pbstrName) );  
            break;  
  
        case mdtAssembly:  
            IfFailGo( GetAssemblyName( pMetaData, dwToken, pbstrName) );  
            break;  
  
        default:  
            ASSERT(!"Unsupported token passed to GetNameFromToken");  
            hr = E_FAIL;  
            break;  
    }  
  
Error:  
  
    METHOD_EXIT(CDebugSymbolProvider::GetNameFromToken, hr);  
    return hr;  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
