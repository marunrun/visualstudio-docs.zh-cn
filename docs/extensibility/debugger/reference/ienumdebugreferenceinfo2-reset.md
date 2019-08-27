---
title: IEnumDebugReferenceInfo2::Reset | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugReferenceInfo2::Reset
helpviewer_keywords:
- IEnumDebugReferenceInfo2::Reset
ms.assetid: cf8ce649-5ce1-44a6-9d5a-89760021bde4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ba76b62f0bf57438db9c7b1b23669c95fe3e3f90
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66324415"
---
# <a name="ienumdebugreferenceinfo2reset"></a>IEnumDebugReferenceInfo2::Reset
将枚举重置为第一个元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Reset(
   void
);
```

```csharp
int Reset();
```

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 调用此方法下, 一步调用后[下一步](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-next.md)方法返回的第一个元素的枚举。

## <a name="see-also"></a>请参阅
- [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)