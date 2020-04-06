---
title: IDebug 突破点请求3 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest3
helpviewer_keywords:
- IDebugBreakpointRequest3
ms.assetid: 8a042beb-b319-48e3-b3c8-9c8336ab371b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 505b0c0b05fa0f14578d770abec6c43ed6b80b01
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734828"
---
# <a name="idebugbreakpointrequest3"></a>IDebugBreakpointRequest3
此接口表示创建和绑定任何类型的断点所需的信息。 它是[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)的扩展名。

## <a name="syntax"></a>语法

```
IDebugBreakpointRequest3 : IDebugBreakpointRequest2
```

## <a name="notes-for-implementers"></a>实施者说明
 会话调试管理器 （SDM） 通常实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
 调试引擎 （DE） 通过在 IDebugBreakpointRequest2 接口上调用在调用[创建挂起断点](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)时收到的[查询接口](/cpp/atl/queryinterface)来访问此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了从[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)继承的方法外，`IDebugBreakpointRequest3`接口还公开了以下方法。

|方法|描述|
|------------|-----------------|
|[GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)|获取描述此断点请求的断点请求信息。|

## <a name="remarks"></a>备注
 此接口用于通过[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)结构向 DE 提供其他信息。 此附加信息包括 DE 的供应商 ID（以 GUID 形式）、跟踪点的名称和断点约束的名称。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
