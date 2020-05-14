---
title: IDebugPointer对象：:De引用 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject::Dereference
helpviewer_keywords:
- IDebugPointerObject::Dereference method
ms.assetid: 196ec2cc-8569-4780-b217-23b24e7f50ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fe87d5db40ce663d84c9561e89a84e6fcb1684ed
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725574"
---
# <a name="idebugpointerobjectdereference"></a>IDebugPointerObject::Dereference
获取指向的对象。

## <a name="syntax"></a>语法

```cpp
HRESULT DeReference( 
   DWORD          dwIndex,
   IDebugObject** ppObject
);
```

```csharp
int Dereference(
   uint             dwIndex,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>参数
`dwIndex`\
[在]指向对象开头的简单字节偏移。

`ppObject`\
[出]返回表示指向的对象的[IDebugObject 对象](../../../extensibility/debugger/reference/idebugobject.md)，以及偏移（如果有）。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。 如果此对象不指向另一个对象，则返回E_FAIL。

## <a name="remarks"></a>备注
 指向的对象可以是基元类型或更复杂的类型，如类或结构。

## <a name="see-also"></a>请参阅
- [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
