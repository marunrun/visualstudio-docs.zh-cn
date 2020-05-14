---
title: IDebug边界断点2：：SetPassCount |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2::SetPassCount
helpviewer_keywords:
- SetPassCount method
- IDebugBoundBreakpoint2::SetPassCount method
ms.assetid: b32c12f9-b34d-43bd-a1b9-61af6cf8e51b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bcc7bd57ce0c392a2874f107c6e4d8d5753399d3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735430"
---
# <a name="idebugboundbreakpoint2setpasscount"></a>IDebugBoundBreakpoint2::SetPassCount
设置或更改与此绑定断点关联的传递计数。

## <a name="syntax"></a>语法

```cpp
HRESULT SetPassCount( 
   BP_PASSCOUNT bpPassCount
);
```

```csharp
int SetPassCount( 
   BP_PASSCOUNT bpPassCount
);
```

## <a name="parameters"></a>参数
`bpPassCount`\
[在]指定通过计数[BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)结构。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。 如果`E_BP_DELETED`绑定断点对象的状态设置为`BPS_DELETED`[（BP_STATE](../../../extensibility/debugger/reference/bp-state.md)枚举的一部分），则返回。

## <a name="remarks"></a>备注
 通过计数确定触发断点时。 可以通过调用[GetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-gethitcount.md)方法获取当前通过计数或命中计数。

 以前与此断点关联的任何通过计数都将丢失。

## <a name="see-also"></a>请参阅
- [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [GetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-gethitcount.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
- [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)
