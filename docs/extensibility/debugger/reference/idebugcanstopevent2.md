---
title: IDebugcanStopevent2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 784bd5b1-4a3f-4455-b313-c4c9a82555a5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f0a3710756f02d7c622be94bab6c3056fb051827
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734510"
---
# <a name="idebugcanstopevent2"></a>IDebugCanStopEvent2
此接口用于询问会话调试管理器 （SDM） 是否在当前代码位置停止。

## <a name="syntax"></a>语法

```
IDebugCanStopEvent2 : IUknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口以支持单步执行源代码。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现（SDM 使用[查询接口](/cpp/atl/queryinterface)访问`IDebugEvent2`接口）。

 此接口的实现必须将 SDM 的[CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)调用传达到调试引擎。 例如，这可以通过发布到调试引擎的消息处理线程的消息来完成，或者实现此接口的对象可以保留对调试引擎的引用，并在将标志传递到`IDebugCanStopEvent2::CanStop`调试引擎时调用回调试引擎。

## <a name="notes-for-callers"></a>呼叫者备注
 每次要求 DE 继续执行 DE 并且 DE 正在单步执行代码时，DE 都可以发送此方法。 此事件使用 SDM 提供的[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)回调功能在附加到正在调试的程序时发送。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugCanStopEvent2`。

|方法|描述|
|------------|-----------------|
|[GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)|获取此事件的原因。|
|[CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)|指定正在调试的程序应在此事件的位置停止（并发送描述停止原因的事件）还是继续执行。|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)|获取描述此事件位置的文档上下文。|
|[GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)|获取描述此事件位置的代码上下文。|

## <a name="remarks"></a>备注
 如果用户踏入函数，并且 DE 发现不存在调试信息或存在调试信息，则 DE 会发送此接口，但 DE 不知道是否可以为该位置显示源代码。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugStepCompleteEvent2](../../../extensibility/debugger/reference/idebugstepcompleteevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
