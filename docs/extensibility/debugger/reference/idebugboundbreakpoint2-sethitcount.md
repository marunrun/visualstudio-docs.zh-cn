---
title: IDebugBound断点2：：SetHitCount |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2::SetHitCount
helpviewer_keywords:
- SetHitCount method
- IDebugBoundBreakpoint2::SetHitCount method
ms.assetid: 8145d875-26b1-4049-a2a2-e7d3d7f4735f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e82f12b12c9afbc24f9416ec2639a4b9768d8fd0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735415"
---
# <a name="idebugboundbreakpoint2sethitcount"></a>IDebugBoundBreakpoint2::SetHitCount
设置绑定断点的命中计数。

## <a name="syntax"></a>语法

```cpp
HRESULT SetHitCount( 
   DWORD dwHitCount
);
```

```csharp
int SetHitCount( 
   uint dwHitCount
);
```

## <a name="parameters"></a>参数
`dwHitCount`\
[在]要设置的命中计数。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。 如果`E_BP_DELETED`绑定断点对象的状态设置为`BPS_DELETED`[（BP_STATE](../../../extensibility/debugger/reference/bp-state.md)枚举的一部分），则返回。

## <a name="remarks"></a>备注
 命中计数是此断点在当前会话运行期间触发的次数。

 调试引擎通常调用此方法来更新此断点的当前命中计数。

## <a name="see-also"></a>请参阅
- [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)
