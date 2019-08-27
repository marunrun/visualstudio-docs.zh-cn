---
title: IDebugCustomAttributeQuery2::IsCustomAttributeDefined |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::IsCustomAttributeDefined
helpviewer_keywords:
- IDebugCustomAttributeQuery2::IsCustomAttributeDefined
ms.assetid: 5c07cc52-6d2d-42df-9d76-9f1f769641db
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0e2ecd70eeeddb4b61d8ed8d307bd579c68ef519
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66335827"
---
# <a name="idebugcustomattributequery2iscustomattributedefined"></a>IDebugCustomAttributeQuery2::IsCustomAttributeDefined
确定名称是否存在自定义属性。

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
[in]包含要查找的自定义属性的名称的字符串。

## <a name="return-value"></a>返回值
 返回 S_OK 如果自定义属性定义此字段，否则，返回 S_FALSE。

## <a name="remarks"></a>备注
 若要获取与自定义属性相关联的属性字节，请调用[GetCustomAttributeByName](../../../extensibility/debugger/reference/idebugcustomattributequery2-getcustomattributebyname.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)