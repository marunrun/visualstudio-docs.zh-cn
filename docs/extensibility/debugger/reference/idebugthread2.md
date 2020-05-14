---
title: IDebugThread2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2
helpviewer_keywords:
- IDebugThread2 interface
ms.assetid: 221b4b1b-4a26-466e-bc29-5eff800fab13
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1965ff1b4cfa89e4584c194942dec7ae486473ff
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718590"
---
# <a name="idebugthread2"></a>IDebugThread2
此接口表示在程序中运行的线程。

## <a name="syntax"></a>语法

```
IDebugThread2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口以表示单个程序中的执行线程。

## <a name="notes-for-callers"></a>呼叫者备注
 调用[GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md)以获取表示当前活动线程的此接口。

 此接口还用于创建断点请求（请参阅[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)）。

 解析绑定或错误断点时也会返回此接口（请参阅[BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)和[BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)）。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugThread2`。

|方法|描述|
|------------|-----------------|
|[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)|检索此线程的堆栈帧的列表。|
|[GetName](../../../extensibility/debugger/reference/idebugthread2-getname.md)|获取线程的名称。|
|[SetThreadName](../../../extensibility/debugger/reference/idebugthread2-setthreadname.md)|设置线程的名称。|
|[GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)|获取运行线程的程序。|
|[CanSetNextStatement](../../../extensibility/debugger/reference/idebugthread2-cansetnextstatement.md)|确定下一个语句是否可以设置为给定的堆栈框架和代码上下文。|
|[SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)|将下一个语句设置到给定的堆栈框架和代码上下文。|
|[GetThreadId](../../../extensibility/debugger/reference/idebugthread2-getthreadid.md)|获取系统线程标识符。|
|[暂停](../../../extensibility/debugger/reference/idebugthread2-suspend.md)|挂起线程。|
|[恢复](../../../extensibility/debugger/reference/idebugthread2-resume.md)|恢复线程。|
|[GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)|获取描述线程的属性。|
|[GetLogicalThread](../../../extensibility/debugger/reference/idebugthread2-getlogicalthread.md)|获取与此物理线程关联的逻辑线程。|

## <a name="remarks"></a>备注
 由于单个物理线程可以在多个程序中运行，因此多个程序中的多个`IDebugThread2`物理线程可以表示相同的物理线程。

 当发生断点或异常时，事件通过调用[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)发送。 此方法的参数之一`IDebugThread2`是表示当前线程的接口。 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)用于获取当前堆栈帧的[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)接口。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
