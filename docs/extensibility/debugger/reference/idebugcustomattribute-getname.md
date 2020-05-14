---
title: IDebug自定义属性：获取名称 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetName
helpviewer_keywords:
- IDebugCustomAttribute::GetName
ms.assetid: ba509cc5-5816-4925-a094-4c72d88c360c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 15d435d043d0e3863358628fa12016431a417918
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732769"
---
# <a name="idebugcustomattributegetname"></a>IDebugCustomAttribute::GetName
获取自定义属性的名称。

## <a name="syntax"></a>语法

```cpp
HRESULT GetName( 
   BSTR* bstrName
);
```

```csharp
int GetName(
   out string bstrName
);
```

## <a name="parameters"></a>参数
`bstrName`\
[出]返回包含自定义属性名称的字符串。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的名称对应于用于声明属性的类的名称。 这可能不完全对应于自定义属性类本身的名称，因为 C# 允许在声明中使用自定义属性名称时从自定义属性名称中删除"属性"后缀。

## <a name="see-also"></a>请参阅
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
