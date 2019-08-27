---
title: IDebugObject::IsReadOnly |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::IsReadOnly
helpviewer_keywords:
- IDebugObject::IsReadOnly method
ms.assetid: c460f772-d08a-4b36-81f3-dff6a51a93fd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 21c8a21f3cc85247f1cef4131768984f99fff764
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349963"
---
# <a name="idebugobjectisreadonly"></a>IDebugObject::IsReadOnly
确定此对象是只读的。

## <a name="syntax"></a>语法

```cpp
HRESULT IsReadOnly( 
   BOOL* pfIsReadOnly
);
```

```csharp
int IsReadOnly(
   out int pfIsReadOnly
);
```

## <a name="parameters"></a>参数
`pfIsReadOnly`\
[out]返回非零值 (`TRUE`) 如果此对象是只读的; 否则为返回零 (`FALSE`)。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 一个只读的对象不能在创建后更改其值。

## <a name="see-also"></a>请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)