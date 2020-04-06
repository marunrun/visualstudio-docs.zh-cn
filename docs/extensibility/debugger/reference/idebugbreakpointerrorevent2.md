---
title: IDebug 突破点错误事件2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointErrorEvent2
helpviewer_keywords:
- IDebugBreakpointErrorEvent2
ms.assetid: adee79df-8db5-4510-a7df-c50f4dbf5e35
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 09cb93f0f16420e56104f371d9caab262873390f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735042"
---
# <a name="idebugbreakpointerrorevent2"></a>IDebugBreakpointErrorEvent2
此接口告诉会话调试管理器 （SDM），由于警告或错误，无法将挂起的断点绑定到加载的程序。

## <a name="syntax"></a>语法

```
IDebugBreakpointErrorEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 DE 实现此接口作为其对断点的支持的一部分。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现（SDM 使用[查询接口](/cpp/atl/queryinterface)访问`IDebugEvent2`接口）。

## <a name="notes-for-callers"></a>呼叫者备注
 当挂起的断点无法绑定到正在调试的程序时，DE 将创建并发送此事件对象。 该事件使用 SDM 提供的[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)回调功能在附加到正在调试的程序时发送。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugBreakpointErrorEvent2`。

|方法|描述|
|------------|-----------------|
|[GetErrorBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)|获取描述警告或错误的[IDebugErrorBreakpointpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)接口。|

## <a name="remarks"></a>备注
 每当绑定断点时，事件都会发送到 SDM。 如果断点无法绑定，则发送`IDebugBreakpointErrorEvent2`。否则，将发送[IDebugBreakpoint 绑定事件 2。](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)

 例如，当与挂起断点关联的条件无法解析或计算时，将发送一条警告，指出此时无法绑定挂起的断点。 如果断点的代码尚未加载，则可能发生此情况。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
