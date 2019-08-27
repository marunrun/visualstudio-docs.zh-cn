---
title: IDebugBreakpointRequest3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest3
helpviewer_keywords:
- IDebugBreakpointRequest3
ms.assetid: 8a042beb-b319-48e3-b3c8-9c8336ab371b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9101f1c2faeedf8b08b3b11044eaa22f6c6d512a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352867"
---
# <a name="idebugbreakpointrequest3"></a>IDebugBreakpointRequest3
此接口表示创建和绑定任何断点类型的所需的信息。 是的扩展[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)。

## <a name="syntax"></a>语法

```
IDebugBreakpointRequest3 : IDebugBreakpointRequest2
```

## <a name="notes-for-implementers"></a>实施者的说明
 会话调试管理器 (SDM) 通常实现此接口。

## <a name="notes-for-callers"></a>调用方的说明
 调试引擎 (DE) 访问此接口通过调用[QueryInterface](/cpp/atl/queryinterface)上的调用中收到的 IDebugBreakpointRequest2 接口[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了继承的方法之外[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)，则`IDebugBreakpointRequest3`接口公开以下方法。

|方法|描述|
|------------|-----------------|
|[GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)|获取描述此断点请求的断点请求信息。|

## <a name="remarks"></a>备注
 此接口用于提供其他信息到通过 DE [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)结构。 此附加信息包括 DE 的供应商 ID （以 GUID 形式）、 跟踪点的名称和断点约束的名称。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)