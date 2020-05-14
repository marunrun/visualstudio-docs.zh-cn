---
title: IDebugObject：：是空引用 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::IsNullReference
helpviewer_keywords:
- IDebugObject::IsNullReference method
ms.assetid: 6dbfcdb0-954f-4486-8fac-7ea8d003e3a9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e4b6e5f2d28d27deb5e4e1ff8278a071ff9110fd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726515"
---
# <a name="idebugobjectisnullreference"></a>IDebugObject::IsNullReference
测试此对象是否为空引用。

## <a name="syntax"></a>语法

```cpp
HRESULT IsNullReference( 
   BOOL* pfIsNull
);
```

```csharp
int IsNullReference(
   out int pfIsNull
);
```

## <a name="parameters"></a>参数
`pfIsNull`\
[出]如果此对象为空`TRUE`引用，则返回非零 （ ）， 则返回非零 （ ）否则，返回零`FALSE`（）。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 空引用表示空对象或尚未分配给的对象。

## <a name="see-also"></a>请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
