---
title: IDebugexception2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2
helpviewer_keywords:
- IDebugExceptionEvent2 interface
ms.assetid: 53d32e59-a84b-4710-833e-c5ab08100516
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cbd53d56b21886e972b33c219367edd603cbf0d5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729778"
---
# <a name="idebugexceptionevent2"></a>IDebugExceptionEvent2
调试引擎 （DE） 在当前正在执行的程序中引发异常时，将此接口发送到会话调试管理器 （SDM）。

## <a name="syntax"></a>语法

```
IDebugExceptionEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 DE 实现此接口以报告正在调试的程序中发生了异常。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现。 SDM 使用[查询接口](/cpp/atl/queryinterface)访问`IDebugEvent2`接口。

## <a name="notes-for-callers"></a>呼叫者备注
 DE 创建并发送此事件对象以报告异常。 该事件使用 SDM 在连接到正在调试的程序时提供的[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)回调函数发送。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugExceptionEvent2`。

|方法|描述|
|------------|-----------------|
|[GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)|获取有关触发此事件的异常的详细信息。|
|[GetExceptionDescription](../../../extensibility/debugger/reference/idebugexceptionevent2-getexceptiondescription.md)|获取引发此事件的异常的人类可读描述。|
|[CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)|确定调试引擎 （DE） 是否支持在恢复执行时将此异常传递给正在调试的程序的选项。|
|[PassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-passtodebuggee.md)|指定是否应将异常传递到执行恢复时正在调试的程序，还是应丢弃该异常。|

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="remarks"></a>备注
 在发送事件之前，DE 会检查此异常事件是否已被以前调用[SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)指定为第一次或第二次异常。 如果已将其指定为第一次异常，则事件`IDebugExceptionEvent2`将发送到 SDM。 如果没有，DE 会给应用程序处理异常的机会。 如果未提供异常处理程序，并且该异常已指定为第二个异常，则事件`IDebugExceptionEvent2`将发送到 SDM。 否则，DE 将恢复执行程序，操作系统或运行时处理异常。

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
