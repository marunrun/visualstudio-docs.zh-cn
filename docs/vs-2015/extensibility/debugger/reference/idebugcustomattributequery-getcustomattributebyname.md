---
title: IDebugCustomAttributeQuery::GetCustomAttributeByName |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugCustomAttributeQuery::GetCustomAttributeByName
- GetCustomAttributeByName
ms.assetid: 6779727c-d10a-4abe-9acd-d0a1eb0737e7
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ff58df26391c3c3fe312f9268f905b4f4f15b858
ms.sourcegitcommit: da4079f5b6ec884baf3108cbd0519d20cb64c70b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62538198"
---
# <a name="idebugcustomattributequerygetcustomattributebyname"></a>IDebugCustomAttributeQuery::GetCustomAttributeByName
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

检索在给定其名称的自定义属性。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetCustomAttributeByName(  
   LPCOLESTR pszCustomAttributeName,  
   BYTE*     ppBlob,  
   DWORD*    pdwLen  
);  
```  
  
```csharp  
int GetCustomAttributeByName(  
   string    pszCustomAttributeName,  
   ref int[] ppBlob,  
   out uint  pdwLen  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszCustomAttributeName`  
 [in]自定义特性的名称。  
  
 `ppBlob`  
 [in、 out]包含自定义特性数据的字节数组。  
  
 `pdwLen`  
 [out]以字节为单位的长度`ppBlob`参数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 如果自定义特性不存在，将返回`S_FALSE`。 否则，返回错误代码。  
  
## <a name="example"></a>示例  
 下面的示例演示如何实现此方法对于**CDebugClassFieldSymbol**对象，它公开[IDebugCustomAttributeQuery](../../../extensibility/debugger/reference/idebugcustomattributequery.md)接口。  
  
```cpp#  
HRESULT CDebugClassFieldSymbol::GetCustomAttributeByName(  
    LPCOLESTR pszCustomAttributeName,  
    BYTE *pBlob,  
    DWORD *pdwLen  
)  
{  
    HRESULT hr = S_FALSE;  
    CComPtr<IMetaDataImport> pMetadata;  
    mdToken token = mdTokenNil;  
    CComPtr<IDebugField> pField;  
    CComPtr<IDebugCustomAttributeQuery> pCA;  
  
    ASSERT(IsValidWideStringPtr(pszCustomAttributeName));  
    ASSERT(IsValidWritePtr(pdwLen, ULONG*));  
  
    METHOD_ENTRY( CDebugClassFieldSymbol::GetCustomAttributeByName );  
  
    IfFalseGo( pszCustomAttributeName && pdwLen, E_INVALIDARG );  
  
    IfFailGo( m_spSH->GetMetadata( m_spAddress->GetModule(), &pMetadata ) );  
  
    IfFailGo( CDebugCustomAttribute::GetTokenFromAddress( m_spAddress, &token) );  
    IfFailGo( CDebugCustomAttribute::GetCustomAttributeByName( pMetadata,  
              token,  
              pszCustomAttributeName,  
              pBlob,  
              pdwLen ) );  
Error:  
  
    METHOD_EXIT( CDebugClassFieldSymbol::GetCustomAttributeByName, hr );  
    return hr;  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [IDebugCustomAttributeQuery](../../../extensibility/debugger/reference/idebugcustomattributequery.md)
