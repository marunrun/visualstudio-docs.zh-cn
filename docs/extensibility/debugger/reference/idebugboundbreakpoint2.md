---
title: IDebugBoundBreakpoint2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2
helpviewer_keywords:
- IDebugBoundBreakpoint2 interface
ms.assetid: df33c52e-ded2-48a0-951d-1f36c8fc922e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 20dbd4ca3f5c56d8519bc6dbfbe362f7904ae56d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350121"
---
# <a name="idebugboundbreakpoint2"></a>IDebugBoundBreakpoint2
此接口表示断点绑定到代码位置。

## <a name="syntax"></a>语法

```
IDebugBoundBreakpoint2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎 (DE) 实现此接口作为断点的支持的一部分。

## <a name="notes-for-callers"></a>调用方的说明
 调用[绑定](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)创建此接口。 调用[GetBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getbreakpoint.md)并[下一步](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-next.md)还可以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugBoundBreakpoint2`。

|方法|描述|
|------------|-----------------|
|[GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)|获取从其创建指定的绑定的断点的挂起断点。|
|[GetState](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)|获取此绑定断点的状态。|
|[GetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-gethitcount.md)|获取此绑定断点的当前命中的计数。|
|[GetBreakpointResolution](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)|获取描述此断点的断点解决方法。|
|[Enable](../../../extensibility/debugger/reference/idebugboundbreakpoint2-enable.md)|启用或禁用断点。|
|[SetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-sethitcount.md)|设置此绑定断点的命中的计数。|
|[SetCondition](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setcondition.md)|设置或更改与此绑定断点相关联的条件。|
|[SetPassCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md)|设置或更改与此绑定断点关联的传递计数。|
|[删除](../../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)|删除断点。|

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [GetBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getbreakpoint.md)
- [下一页](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-next.md)
- [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)