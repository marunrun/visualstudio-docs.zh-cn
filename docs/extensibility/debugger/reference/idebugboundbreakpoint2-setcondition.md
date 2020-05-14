---
title: IDebug边界断点2：：设置条件 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2::SetCondition
helpviewer_keywords:
- SetCondition method
- IDebugBoundBreakpoint2::SetCondition method
ms.assetid: 5d366876-efed-43d0-8ea1-dfdb009cbfac
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f23fbe1b353378ca521fa802bdeae25fd12476df
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735461"
---
# <a name="idebugboundbreakpoint2setcondition"></a>IDebugBoundBreakpoint2::SetCondition
设置或更改与此绑定断点关联的条件。

## <a name="syntax"></a>语法

```cpp
HRESULT SetCondition( 
   BP_CONDITION bpCondition
);
```

```csharp
int SetCondition( 
   enum_BP_CONDITION bpCondition
);
```

## <a name="parameters"></a>参数
`bpCondition`\
[在]描述条件[BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)枚举中的值。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。 如果`E_BP_DELETED`绑定断点对象的状态设置为`BPS_DELETED`[（BP_STATE](../../../extensibility/debugger/reference/bp-state.md)枚举的一部分），则返回。

## <a name="remarks"></a>备注
 以前与此断点关联的任何条件都将丢失。

## <a name="see-also"></a>请参阅
- [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
- [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)
