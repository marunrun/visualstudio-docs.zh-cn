---
title: IDebugPendingBreakpoint2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2
helpviewer_keywords:
- IDebugPendingBreakpoint2 interface
ms.assetid: d416b095-917e-475e-b796-ec0a03ffb8da
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1581620d2a26b8717a1c84399e43463b9312a96d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66308792"
---
# <a name="idebugpendingbreakpoint2"></a>IDebugPendingBreakpoint2
此接口表示断点已准备好将绑定到代码位置。

## <a name="syntax"></a>语法

```
IDebugPendingBreakpoint2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎 (DE) 实现此接口作为断点的支持的一部分。

## <a name="notes-for-callers"></a>调用方的说明
 调用[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)创建从挂起断点[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)接口。 调用[绑定](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)创建`IDebugBreakpoint2`表示在程序中的绑定的断点的接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugPendingBreakpoint2`。

|方法|描述|
|------------|-----------------|
|[CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|确定此挂起断点是否可将绑定到代码位置。|
|[Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|将此挂起断点绑定到一个或多个代码位置。|
|[GetState](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|获取此挂起断点的状态。|
|[GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|获取用于创建此挂起断点的断点请求。|
|[Virtualize](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)|切换此挂起断点的虚拟化的状态。|
|[Enable](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)|切换此挂起断点的启用的状态。|
|[SetCondition](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setcondition.md)|设置或更改与此相关联挂起断点的条件。|
|[SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md)|设置或更改与此挂起断点关联的传递计数。|
|[EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|枚举绑定中此挂起断点的所有断点。|
|[EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|枚举源自此挂起断点的所有错误断点。|
|[删除](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|删除此挂起断点和从该绑定的所有断点。|

## <a name="remarks"></a>备注
 `IDebugPendingBreakpoint2` 可以认为的将断点绑定到可以应用于一个或多个程序的代码所需的所有必要信息的提供程序。

 挂起断点可能会生成多个绑定的断点。 例如中的断点C++的样式模板可能会生成有关该模板的每个唯一实例绑定的断点。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)