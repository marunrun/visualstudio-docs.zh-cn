---
title: IEnum调试程序2：：克隆 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPrograms2::Clone
helpviewer_keywords:
- IEnumDebugPrograms2::Clone
ms.assetid: 880846c2-39d3-45cd-85c3-ad5409a3710f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 26a099e84414afaf84d2505b35327ed86e125292
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715731"
---
# <a name="ienumdebugprograms2clone"></a>IEnumDebugPrograms2::Clone
将当前枚举的副本作为单独的对象返回。

## <a name="syntax"></a>语法

```cpp
HRESULT Clone(
   IEnumDebugPrograms2** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugPrograms2 ppEnum
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
- [IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)
