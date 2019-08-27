---
title: IDebugAlias::Dispose |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAlias::Dispose
helpviewer_keywords:
- IDebugAlias::Dispose method
ms.assetid: e84909a4-d378-4f48-bf25-2c014c77c8e3
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c84fc6887eb2594f9665924bd3eafa5452a3135c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66330280"
---
# <a name="idebugaliasdispose"></a>IDebugAlias::Dispose
将标记为删除此别名。

## <a name="syntax"></a>语法

```cpp
HRESULT Dispose();
```

```csharp
int Dispose();
```

## <a name="parameters"></a>参数
 无。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 一旦调用此方法，该别名不再可用。

## <a name="see-also"></a>请参阅
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)