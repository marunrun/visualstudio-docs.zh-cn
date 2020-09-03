---
title: IDebugCustomAttributeQuery2：： IsCustomAttributeDefined |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::IsCustomAttributeDefined
helpviewer_keywords:
- IDebugCustomAttributeQuery2::IsCustomAttributeDefined
ms.assetid: 5c07cc52-6d2d-42df-9d76-9f1f769641db
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7be649a5d65f88d8263bbe8950fda1a157855ed2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80732532"
---
# <a name="idebugcustomattributequery2iscustomattributedefined"></a>IDebugCustomAttributeQuery2::IsCustomAttributeDefined
确定是否存在按名称的自定义属性。

## <a name="syntax"></a>语法

```cpp
HRESULT IsCustomAttributeDefined( 
   LPCOLESTR pszCustomAttributeName
);
```

```csharp
int IsCustomAttributeDefined(
   [In] string pszCustomAttributeName
);
```

## <a name="parameters"></a>参数
`pszCustomAttributeName`\
中一个字符串，其中包含要查找的自定义特性的名称。

## <a name="return-value"></a>返回值
 如果在此字段上定义了自定义特性，则返回 S_OK; 否则，将返回 S_FALSE。

## <a name="remarks"></a>备注
 若要获取与自定义属性关联的属性字节，请调用 [GetCustomAttributeByName](../../../extensibility/debugger/reference/idebugcustomattributequery2-getcustomattributebyname.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
