---
title: IDebugEventCallback2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEventCallback2
helpviewer_keywords:
- IDebugEventCallback2
ms.assetid: 2c935ee0-2e22-4be0-a852-73736f33c8c9
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e3d76c3e41159e9bc200acdb788c13ad5f995cc3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310516"
---
# <a name="idebugeventcallback2"></a>IDebugEventCallback2
此接口由调试引擎 (DE) 用于将调试事件发送到会话调试管理器 (SDM)。

## <a name="syntax"></a>语法

```
IDebugEventCallback2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 实现此接口以接收来自调试引擎的事件。

## <a name="notes-for-callers"></a>调用方的说明
 调试引擎通常接收此接口，当调用 SDM[附加](../../../extensibility/debugger/reference/idebugprogram2-attach.md)，[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)，或[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)。 调试引擎通过调用将事件发送到 SDM[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugEventCallback2`。

|方法|描述|
|------------|-----------------|
|[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)|发送通知的调试 SDM 的事件。|

## <a name="remarks"></a>备注
 尽管[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)并[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)指定它们采用`IDebugEventCallback2`接口，这种情况下，并不接口指针将始终为 null 值。 相反，必须使用调试引擎`IDebugEventCallback2`接口对的调用中接收[附加](../../../extensibility/debugger/reference/idebugprogram2-attach.md)，[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)，或[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)。

 如果包实现[IDebugEventCallback](../../../extensibility/debugger/reference/idebugeventcallback2.md)在托管代码中，我们强烈建议对该<xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A>传递给各种接口上调用[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [附加](../../../extensibility/debugger/reference/idebugprogram2-attach.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)