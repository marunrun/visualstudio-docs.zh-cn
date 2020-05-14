---
title: IDebug 待定断点2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2
helpviewer_keywords:
- IDebugPendingBreakpoint2 interface
ms.assetid: d416b095-917e-475e-b796-ec0a03ffb8da
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4e6f2c1df37e953a5d8c66bad9d0a3574a463fad
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725648"
---
# <a name="idebugpendingbreakpoint2"></a>IDebugPendingBreakpoint2
此接口表示准备绑定到代码位置的断点。

## <a name="syntax"></a>语法

```
IDebugPendingBreakpoint2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口作为其对断点的支持的一部分。

## <a name="notes-for-callers"></a>呼叫者备注
 对[创建挂起断点的](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)调用从[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)接口创建一个挂起的断点。 对[Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)的调用`IDebugBreakpoint2`将创建表示程序中的绑定断点的接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugPendingBreakpoint2`。

|方法|描述|
|------------|-----------------|
|[CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|确定此挂起的断点是否可以绑定到代码位置。|
|[绑定](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|将此挂起的断点绑定到一个或多个代码位置。|
|[获取状态](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|获取此挂起断点的状态。|
|[GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|获取用于创建此挂起断点的断点请求。|
|[Virtualize](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)|切换此挂起断点的虚拟化状态。|
|[启用](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)|切换此挂起断点的启用状态。|
|[SetCondition](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setcondition.md)|设置或更改与此挂起的断点关联的条件。|
|[SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md)|设置或更改与此挂起的断点关联的传递计数。|
|[EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|枚举从此挂起的断点绑定的所有断点。|
|[EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|枚举此挂起断点产生的所有错误断点。|
|[删除](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|删除此挂起的断点和所有从其绑定的断点。|

## <a name="remarks"></a>备注
 `IDebugPendingBreakpoint2`可以认为是绑定断点到可应用于一个或多个程序的代码所需的所有信息的提供者。

 挂起的断点可能会生成多个绑定断点。 例如，C++样式模板中的断点可以为该模板的每个唯一实例生成绑定断点。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)
