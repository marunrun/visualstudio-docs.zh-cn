---
title: IDebugBreakpointRequest2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 01ac4013-96f9-4235-b289-f55f9e99558f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 55e7c73b720e326b823c3038928d7141ea732155
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352927"
---
# <a name="idebugbreakpointrequest2"></a>IDebugBreakpointRequest2
此接口表示创建和绑定任何断点类型的所需的信息。

## <a name="syntax"></a>语法

```
IDebugBreakpointRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 会话调试管理器 (SDM) 通常实现此接口。

## <a name="notes-for-callers"></a>调用方的说明
 调试引擎 (DE) 接收通过调用此接口[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)为了创建挂起断点。 调用[GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)可以从设备中检索此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugBreakpointRequest2`。

|方法|描述|
|------------|-----------------|
|[GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md)|获取此断点请求的断点位置类型。|
|[GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)|获取描述此断点请求的断点请求信息。|

## <a name="remarks"></a>备注
 之后该程序正在调试已加载，调用[绑定](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)将挂起断点绑定到程序中请求的位置。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)
- [GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)
- [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)