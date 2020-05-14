---
title: IDebugEvent回拨2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEventCallback2
helpviewer_keywords:
- IDebugEventCallback2
ms.assetid: 2c935ee0-2e22-4be0-a852-73736f33c8c9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a74825a955afdde03e63673c4b1b6afda5904953
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729884"
---
# <a name="idebugeventcallback2"></a>IDebugEventCallback2
调试引擎 （DE） 使用此接口向会话调试管理器 （SDM） 发送调试事件。

## <a name="syntax"></a>语法

```
IDebugEventCallback2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]实现此接口以从调试引擎接收事件。

## <a name="notes-for-callers"></a>呼叫者备注
 当 SDM 调用[附加](../../../extensibility/debugger/reference/idebugprogram2-attach.md)、[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)或[启动挂起](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)时，调试引擎通常会接收此接口。 调试引擎通过调用[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)向 SDM 发送事件。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugEventCallback2`。

|方法|描述|
|------------|-----------------|
|[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)|向 SDM 发送调试事件通知。|

## <a name="remarks"></a>备注
 尽管[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)和[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)指定`IDebugEventCallback2`它们采用接口，但事实并非如此，并且接口指针将始终为空值。 相反，调试引擎必须使用调用中`IDebugEventCallback2`收到的接口来[连接](../../../extensibility/debugger/reference/idebugprogram2-attach.md)、[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)或[启动暂停](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)。

 如果包在托管代码中实现[IDebugEvent 回调](../../../extensibility/debugger/reference/idebugeventcallback2.md)，强烈建议<xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A>在传递给[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)的各种接口上调用 。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
