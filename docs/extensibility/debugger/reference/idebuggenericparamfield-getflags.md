---
title: IDebugGenericParamField::GetFlags | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetFlags
- IDebugGenericParamField::GetFlags
ms.assetid: adcbbca1-8960-4c88-86b0-8b9467056c97
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 17e3bbf128483ab7a3a63c328f4ce3e77095714f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66320803"
---
# <a name="idebuggenericparamfieldgetflags"></a>IDebugGenericParamField::GetFlags
检索此泛型参数的标志。

## <a name="syntax"></a>语法

```cpp
HRESULT GetFlags(
    DWORD* pdwFlags
);
```

```csharp
int GetFlags(
    ref uint pdwFlags
);
```

## <a name="parameters"></a>参数
`pdwFlags`\
[out]返回此泛型参数的标志。

## <a name="return-value"></a>返回值
如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
这些标志包含有关各种特殊约束的信息。

## <a name="example"></a>示例
下面的示例演示如何实现此方法对于**CDebugGenericParamFieldType**对象，它公开[IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)接口。

```cpp
HRESULT CDebugGenericParamFieldType::GetFlags(DWORD *pdwFlags)
{
    HRESULT hr = S_OK;

    METHOD_ENTRY( CDebugGenericParamFieldType::GetFlags );

    IfFalseGo( pdwFlags, E_INVALIDARG );
    IfFailGo( this->LoadProps() );
    *pdwFlags = m_dwFlags;

Error:

    METHOD_EXIT( CDebugGenericParamFieldType::GetFlags, hr );
    return hr;
}
```

## <a name="see-also"></a>请参阅
- [IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)
