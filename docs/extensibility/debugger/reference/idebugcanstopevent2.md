---
title: IDebugCanStopEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 784bd5b1-4a3f-4455-b313-c4c9a82555a5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ab364b426005c838072fabc1a3c7ed2f7d64ac6a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66337333"
---
# <a name="idebugcanstopevent2"></a>IDebugCanStopEvent2
使用此接口要求会话调试管理器 (SDM) 是否在当前代码位置停止。

## <a name="syntax"></a>语法

```
IDebugCanStopEvent2 : IUknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎 (DE) 实现此接口以支持单步执行源代码。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象 (使用 SDM [QueryInterface](/cpp/atl/queryinterface)访问`IDebugEvent2`接口)。

 此接口的实现必须进行通信的 SDM 的调用[CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)到调试引擎。 例如，这可以通过一条消息发布到调试引擎的消息处理线程或实现此接口的对象无法保存对调试引擎的引用并回调到调试引擎传递到标志`IDebugCanStopEvent2::CanStop`。

## <a name="notes-for-callers"></a>调用方的说明
 DE 可以发送此方法每次 DE 需要继续执行，DE 逐句通过代码。 通过使用发送此事件[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 它附加到正在调试的程序时所提供的回调函数。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugCanStopEvent2`。

|方法|描述|
|------------|-----------------|
|[GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)|获取此事件的原因。|
|[CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)|指定是否正在调试的程序应在此事件 （和发送描述停止的原因的事件） 的位置停止，或只需继续执行。|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)|获取用于描述此事件的位置的文档上下文。|
|[GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)|获取用于描述此事件的位置的代码上下文。|

## <a name="remarks"></a>备注
 如果用户单步执行函数，DE 查找任何调试信息或调试信息存在但 DE 不知道如果可以对该位置显示的源代码，DE 发送此接口。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugStepCompleteEvent2](../../../extensibility/debugger/reference/idebugstepcompleteevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)