---
title: IDebugCustomAttributeQuery::GetCustomAttributeByName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugCustomAttributeQuery::GetCustomAttributeByName
- GetCustomAttributeByName
ms.assetid: 6779727c-d10a-4abe-9acd-d0a1eb0737e7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: df4dfa880104b9989e49761beb823c960de85391
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66346061"
---
# <a name="idebugcustomattributequerygetcustomattributebyname"></a>IDebugCustomAttributeQuery::GetCustomAttributeByName
检索在给定其名称的自定义属性。

## <a name="syntax"></a>语法

```cpp
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

## <a name="parameters"></a>参数
`pszCustomAttributeName`\
[in]自定义特性的名称。

`ppBlob`\
[in、 out]包含自定义特性数据的字节数组。

`pdwLen`\
[out]以字节为单位的长度`ppBlob`参数。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK`。 如果自定义特性不存在，将返回`S_FALSE`。 否则，返回错误代码。

## <a name="example"></a>示例
下面的示例演示如何实现此方法对于**CDebugClassFieldSymbol**对象，它公开[IDebugCustomAttributeQuery](../../../extensibility/debugger/reference/idebugcustomattributequery.md)接口。

```cpp
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
- [IDebugCustomAttributeQuery](../../../extensibility/debugger/reference/idebugcustomattributequery.md)
