---
title: IDebugAlias：:D微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAlias::Dispose
helpviewer_keywords:
- IDebugAlias::Dispose method
ms.assetid: e84909a4-d378-4f48-bf25-2c014c77c8e3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: df3a2ecc50063df8f90645b9ccaa72754c3728c1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736556"
---
# <a name="idebugaliasdispose"></a>IDebugAlias::Dispose
标记此别名以进行删除。

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
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法后，别名将不再可用。

## <a name="see-also"></a>请参阅
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
