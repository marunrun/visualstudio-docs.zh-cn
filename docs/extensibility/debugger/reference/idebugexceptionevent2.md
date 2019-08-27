---
title: IDebugExceptionEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2
helpviewer_keywords:
- IDebugExceptionEvent2 interface
ms.assetid: 53d32e59-a84b-4710-833e-c5ab08100516
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3fd2a449c71b69c654cd19846990f7b722f706de
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66325983"
---
# <a name="idebugexceptionevent2"></a>IDebugExceptionEvent2
在当前正在执行的程序中引发异常时，调试引擎 (DE) 会将此接口发送到会话调试管理器 (SDM)。

## <a name="syntax"></a>语法

```
IDebugExceptionEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 DE 实现此接口向报表中正在调试的程序出现异常。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象。 使用 SDM [QueryInterface](/cpp/atl/queryinterface)访问`IDebugEvent2`接口。

## <a name="notes-for-callers"></a>调用方的说明
 DE 创建并发送此事件对象报告异常。 使用发送该事件[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 它附加到正在调试的程序时提供的回调函数。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugExceptionEvent2`。

|方法|描述|
|------------|-----------------|
|[GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)|获取有关激发此事件的异常的详细的信息。|
|[GetExceptionDescription](../../../extensibility/debugger/reference/idebugexceptionevent2-getexceptiondescription.md)|获取引发的异常触发此事件的用户可读说明。|
|[CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)|确定调试引擎 (DE) 支持将此异常传递给执行恢复时正在调试的程序的选项。|
|[PassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-passtodebuggee.md)|指定异常应传递到时恢复执行，正在调试的程序还是应放弃该异常。|

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>备注
 在发送前事件，检查以确定是否此异常事件已被指定首次异常或二次异常通过以前调用 DE [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)。 如果已指定为最可能的异常，`IDebugExceptionEvent2`事件发送到 SDM。 如果没有，DE 使应用程序有机会处理异常。 如果未不提供任何异常处理程序，并且如果异常已被指定为第二个可能发生的异常，`IDebugExceptionEvent2`事件发送到 SDM。 否则为 DE 继续执行程序，并且操作系统或运行时处理异常。

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)