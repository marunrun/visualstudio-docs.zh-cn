---
title: IDebugStackFrame3 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame3
helpviewer_keywords:
- IDebugStackFrame3 interface
ms.assetid: 39af2f57-0a01-42b8-b093-b7fbc61e2909
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d86997d11e124fd5a47981314cf383f5cd8aff7d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719468"
---
# <a name="idebugstackframe3"></a>IDebugStackFrame3
此接口扩展[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)以处理截获的异常。

## <a name="syntax"></a>语法

```
IDebugStackFrame3 : IDebugStackFrame2
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 在实现[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)接口以支持截获的异常的同一对象上实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
 在`IDebugStackFrame2`接口上调用[查询接口](/cpp/atl/queryinterface)以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了从[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)继承的方法外，`IDebugStackFrame3`还公开了以下方法。

|方法|描述|
|------------|-----------------|
|[InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)|在任何常规异常处理之前处理当前堆栈帧的异常。|
|[GetUnwindCodeContext](../../../extensibility/debugger/reference/idebugstackframe3-getunwindcodecontext.md)|如果要进行堆栈展开，则返回代码上下文。|

## <a name="remarks"></a>备注
 截获的异常意味着调试器可以在运行时调用任何正常异常处理例程之前处理异常。 拦截异常实质上意味着使运行时假装存在异常处理程序，即使没有异常处理程序。

- 在所有正常异常回调事件（唯一的例外是调试混合模式代码（托管和非托管代码）期间调用[InterceptCurrentException，](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)在这种情况下，在最后一次回叫期间无法截获异常）。 如果 DE 未实现`IDebugStackFrame3`，或者 DE 返回 IDebugStackFrame3：：（`InterceptCurrentException`如`E_NOTIMPL`）的错误，则调试器将正常处理异常。

 通过拦截异常，调试器可以允许用户对正在调试的程序的状态进行更改，然后在引发异常时恢复执行。

> [!NOTE]
> 仅在托管代码中允许截获的异常，即在"通用语言运行时 （CLR）"下运行的程序中允许截获的异常。

 调试引擎表示它支持通过使用`SetMetric`函数在运行时将"metricExceptions"设置为 1 的值来拦截异常。 有关详细信息，请参阅[用于调试 的 SDK 帮助器](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [用于调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
