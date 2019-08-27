---
title: IDebugObject::SetValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::SetValue
helpviewer_keywords:
- IDebugObject::SetValue method
ms.assetid: d652e09c-cdc1-4519-8116-d7c743f5679b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a9c6590c45027eb3dce28e2dbac182a967e87d59
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66318949"
---
# <a name="idebugobjectsetvalue"></a>IDebugObject::SetValue
设置对象的值从一系列连续的字节数。

## <a name="syntax"></a>语法

```cpp
HRESULT SetValue( 
   BYTE* pValue,
   UINT  nSize
);
```

```csharp
int SetValue(
   byte[] pValue,
   uint   nSize
);
```

## <a name="parameters"></a>参数
`pValue`\
[in]一个表示新值的字节数组。

`nSize`\
[in]以字节为单位的值的大小。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 数组中的值复制到此[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)对象，并将任何现有值替换。 新值的大小可大于或小于现有值。 这`IDebugObject`不能为 null 引用。

## <a name="see-also"></a>请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)