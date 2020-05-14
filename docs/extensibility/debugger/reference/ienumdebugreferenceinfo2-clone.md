---
title: IEnumDebug参考信息2：：克隆 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugReferenceInfo2::Clone
helpviewer_keywords:
- IEnumDebugReferenceInfo2::Clone
ms.assetid: 49c5a301-a33a-428f-b83b-e734c71af4ef
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d522fb7a9b63f634f312924e3c0b0337688aa430
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715307"
---
# <a name="ienumdebugreferenceinfo2clone"></a>IEnumDebugReferenceInfo2::Clone
将当前枚举的副本作为单独的对象返回。

## <a name="syntax"></a>语法

```cpp
HRESULT Clone(
   IEnumDebugReferenceInfo2** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugReferenceInfo2 ppEnum
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
- [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)
