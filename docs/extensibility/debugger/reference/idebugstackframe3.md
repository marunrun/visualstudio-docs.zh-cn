---
title: IDebugStackFrame3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame3
helpviewer_keywords:
- IDebugStackFrame3 interface
ms.assetid: 39af2f57-0a01-42b8-b093-b7fbc61e2909
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0960f0f527d844afcc44947f1204db78d4d91a38
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352062"
---
# <a name="idebugstackframe3"></a>IDebugStackFrame3
此接口扩展[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)来处理已截获的异常。

## <a name="syntax"></a>语法

```
IDebugStackFrame3 : IDebugStackFrame2
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎 (DE) 实现此接口上实现的相同对象[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)接口以支持已截获的异常。

## <a name="notes-for-callers"></a>调用方的说明
 调用[QueryInterface](/cpp/atl/queryinterface)上`IDebugStackFrame2`接口，以获得此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了继承的方法之外[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)，`IDebugStackFrame3`公开以下方法。

|方法|描述|
|------------|-----------------|
|[InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)|处理当前堆栈帧之前任何常规异常处理的异常。|
|[GetUnwindCodeContext](../../../extensibility/debugger/reference/idebugstackframe3-getunwindcodecontext.md)|出现堆栈展开时，返回代码上下文。|

## <a name="remarks"></a>备注
 已截获的异常意味着运行时在调用任何常规异常处理例程之前调试程序，可以处理异常。 实质上截获异常意味着使假设是存在，即使没有异常处理程序的运行的时间。

- [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)在普通的异常的所有回调事件期间调用 (唯一的例外情况是如果在进行调试混合模式代码 （托管和非托管代码），在这种情况下不能在过程截获异常最后一个回调）。 如果未执行 DE `IDebugStackFrame3`，或 DE 从 IDebugStackFrame3 返回错误::`InterceptCurrentException` (如`E_NOTIMPL`)，则调试器将正常处理此异常。

 通过截获异常，调试器可以允许用户对正在调试的程序的状态进行更改，然后继续执行在引发异常的点。

> [!NOTE]
> 已截获的异常只允许出现在托管代码中，即，在程序运行在公共语言运行时 (CLR) 中。

 调试引擎，它支持通过设置"metricExceptions"截取异常为值 1 在运行时通过使用指示`SetMetric`函数。 有关详细信息，请参阅[以便进行调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [用于调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
