---
title: IDebugObject2::GetBackingFieldForProperty |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::GetBackingFieldForProperty
helpviewer_keywords:
- IDebugObject2::GetBackingFieldForProperty method
ms.assetid: e72c6338-5573-4fad-8075-f3ade3435424
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9aaf4111670ad67f6a01bde60bf5f35c3b793983
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66317343"
---
# <a name="idebugobject2getbackingfieldforproperty"></a>IDebugObject2::GetBackingFieldForProperty
获取字段或变量 （如果有），可能会支持此对象表示的属性。

## <a name="syntax"></a>语法

```cpp
HRESULT GetBackingFieldForProperty(
   IDebugObject2** ppObject
);
```

```csharp
int GetBackingFieldForProperty(
   out IDebugObject2 ppObject
);
```

## <a name="parameters"></a>参数
`ppObject`\
[out][IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)描述支持字段的对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)对象表示一个托管的代码的类属性，即使用 get 方法和/或 set 访问器。 此类属性通常需要一个变量来包含由属性操作的值。 此变量被称为支持字段。 如果该对象不支持字段，则请确保将返回 null 值： 某些调用方可能没有注意到返回的值，但将改为查找以查看是否在已返回 null 值`ppObject`。

## <a name="see-also"></a>请参阅
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)