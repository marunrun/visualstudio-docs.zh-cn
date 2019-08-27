---
title: IDebugObject2::GetAlias | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::GetAlias
helpviewer_keywords:
- IDebugObject2::GetAlias method
ms.assetid: aa6824d5-c932-42ba-8713-950e7d1fb42f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: db9156e01843e859a2279e43f73c00bee21b3e9c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66308746"
---
# <a name="idebugobject2getalias"></a>IDebugObject2::GetAlias
如果有，获取与此对象相关联的别名。

## <a name="syntax"></a>语法

```cpp
HRESULT GetAlias(
   IDebugAlias** ppAlias
);
```

```csharp
int GetAlias(
   out IDebugAlias ppAlias
);
```

## <a name="parameters"></a>参数
`ppAlias`\
[out]返回[IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)对象，表示此对象的别名; 否则，返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 通过调用创建一个对象的别名[CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)