---
title: IEnumDebugPort供应商2：：克隆 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPortSuppliers2::Clone
helpviewer_keywords:
- IEnumDebugPortSuppliers2::Clone
ms.assetid: 98b9914d-4f32-44da-b422-68830bce44b4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bc6dc6c055f9821c9c7f02312762d3dd0a44bc58
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716095"
---
# <a name="ienumdebugportsuppliers2clone"></a>IEnumDebugPortSuppliers2::Clone
将当前枚举的副本作为单独的对象返回。

## <a name="syntax"></a>语法

```cpp
HRESULT Clone(
   IEnumDebugPortSuppliers2** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugPortSuppliers2 ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
[出]将此枚举的副本作为单独的对象返回。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 枚举的副本在调用此方法时与原始副本具有相同的状态。 但是，副本和原始副本的状态是分开的，可以单独更改。

## <a name="see-also"></a>请参阅
- [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md)
