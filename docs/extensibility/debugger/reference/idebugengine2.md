---
title: IDebugEngine2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2
helpviewer_keywords:
- IDebugEngine2 interface
ms.assetid: 1f0e9ac0-6dfb-461a-976c-888d82144cdb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5e00751db052adeefee828829ec89309a3adba4b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80730861"
---
# <a name="idebugengine2"></a>IDebugEngine2
此接口表示 (DE) 的调试引擎。 它用于管理调试会话的各个方面，从创建断点到设置和清除异常。

## <a name="syntax"></a>语法

```
IDebugEngine2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 此接口由自定义 DE 实现，用于管理程序调试。 此接口必须由 DE 实现。

## <a name="notes-for-callers"></a>调用方说明
 此接口由会话调试管理器 (SDM) 调用，用于管理调试会话，包括管理异常、创建断点以及响应 DE 发送的同步事件。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugEngine2` 。

|方法|说明|
|------------|-----------------|
|[EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)|为通过 DE 调试的所有程序创建一个枚举器。|
|[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)|将 DE 附加到节目。|
|[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)|在 DE 中创建挂起断点。|
|[SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)|指定 DE 应如何处理给定的异常。|
|[RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)|删除指定的异常，以使其不再由调试引擎处理。|
|[RemoveAllSetExceptions](../../../extensibility/debugger/reference/idebugengine2-removeallsetexceptions.md)|删除 IDE 为特定运行时体系结构或语言设置的异常列表。|
|[GetEngineID](../../../extensibility/debugger/reference/idebugengine2-getengineid.md)|获取 DE 的 GUID。|
|[DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)|通知解除了指定的程序已被异常终止，并应清除对程序的所有引用并发送程序销毁事件。|
|[ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)|由 SDM 调用，用于指示已接收并处理以前由 DE 发送到 SDM 的同步调试事件。|
|[SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)|设置取消的区域设置。|
|[SetRegistryRoot](../../../extensibility/debugger/reference/idebugengine2-setregistryroot.md)|设置 DE 当前正在使用的注册表根。|
|[SetMetric](../../../extensibility/debugger/reference/idebugengine2-setmetric.md)|设置指标。|
|[CauseBreak](../../../extensibility/debugger/reference/idebugengine2-causebreak.md)|请求此 DE 正在调试的所有程序将在下一次尝试运行的线程时停止执行。|

## <a name="requirements"></a>要求
 标头： Msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [GetEngine](../../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md)
