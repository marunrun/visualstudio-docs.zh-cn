---
title: IDebugObject：设置值 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::SetValue
helpviewer_keywords:
- IDebugObject::SetValue method
ms.assetid: d652e09c-cdc1-4519-8116-d7c743f5679b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9e4652eb3c77a1871063dfa71b464fb1f7c43f94
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726366"
---
# <a name="idebugobjectsetvalue"></a>IDebugObject::SetValue
设置连续字节序列中对象的值。

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
[在]表示新值的字节数组。

`nSize`\
[在]值的大小（以字节为单位）。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 数组中的值将复制到此[IDebugObject 对象](../../../extensibility/debugger/reference/idebugobject.md)中，替换任何现有值。 新值的大小可以大于或小于现有值。 这`IDebugObject`不能为空引用。

## <a name="see-also"></a>请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)
