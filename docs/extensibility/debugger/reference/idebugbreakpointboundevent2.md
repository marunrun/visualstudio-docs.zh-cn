---
title: IDebugBreakpointBoundEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointBoundEvent2
helpviewer_keywords:
- IDebugBreakpointBoundEvent2
ms.assetid: 24ba362e-5be1-481a-b071-e1ebd3cae6e8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: be8b87aabe10861f53c3c40b4fce78dac9a9adc4
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66314295"
---
# <a name="idebugbreakpointboundevent2"></a>IDebugBreakpointBoundEvent2
此接口通知会话调试管理器 (SDM) 已成功向加载程序绑定挂起断点。

## <a name="syntax"></a>语法

```
IDebugBreakpointBoundEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 DE 实现此接口作为断点的支持的一部分。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象 (使用 SDM [QueryInterface](/cpp/atl/queryinterface)访问`IDebugEvent2`接口)。

## <a name="notes-for-callers"></a>调用方的说明
 DE 创建，并挂起断点成功绑定到正在调试的程序时发送此事件对象。 通过使用发送该事件[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 它附加到正在调试的程序时所提供的回调函数。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugBreakpointBoundEvent2`。

|方法|描述|
|------------|-----------------|
|[GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)|获取要绑定的挂起断点。|
|[EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)|创建已绑定到此事件的断点的枚举器。|

## <a name="remarks"></a>备注
 只要绑定断点，则将事件发送到 SDM。 如果无法绑定断点， [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)发送; 否则为`IDebugBreakpointBoundEvent2`发送。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)