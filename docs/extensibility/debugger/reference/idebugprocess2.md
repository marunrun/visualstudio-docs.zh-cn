---
title: IDebugProcess2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2
helpviewer_keywords:
- IDebugProcess2 interface
ms.assetid: 99f6cd06-4076-45ee-b2ae-fa2ad627fd18
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c72659491ec6718397a4fbb494175eea0896c7f7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80723797"
---
# <a name="idebugprocess2"></a>IDebugProcess2
此接口表示在端口上运行的进程。 如果端口为本地端口，则 `IDebugProcess2` 通常表示本地计算机上的物理进程。

## <a name="syntax"></a>语法

```
IDebugProcess2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 此接口由自定义端口提供程序实现，以将程序作为组进行管理。 此接口必须由端口提供程序实现。

 如果调试引擎支持通过 [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)启动程序，则它还会实现此接口。

## <a name="notes-for-callers"></a>调用方说明
 此接口主要由会话调试管理器 (SDM) 调用，以便与在此进程中标识的一组程序进行交互。

 调用 [GetProcess](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md) 或 [GetProcess](../../../extensibility/debugger/reference/idebugport2-getprocess.md) 以获取此接口。 此接口还通过调用返回 `IDebugEngineLaunch2::LaunchSuspended` 。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugProcess2` 。

|方法|说明|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)|获取进程的说明。|
|[EnumPrograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)|枚举此进程中包含的程序。|
|[GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)|获取进程的标题、友好名称或文件名。|
|[GetServer](../../../extensibility/debugger/reference/idebugprocess2-getserver.md)|获取此进程正在其上运行的计算机服务器的实例。|
|Terminate|终止进程。|
|[附加](../../../extensibility/debugger/reference/idebugprocess2-attach.md)|附加到进程。|
|[CanDetach](../../../extensibility/debugger/reference/idebugprocess2-candetach.md)|确定 SDM 是否可以分离进程。|
|[分离](../../../extensibility/debugger/reference/idebugprocess2-detach.md)|将调试器与进程分离。|
|[GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)|获取系统进程标识符。|
|[GetProcessId](../../../extensibility/debugger/reference/idebugprocess2-getprocessid.md)|获取此进程的全局唯一标识符。|
|[GetAttachedSessionName](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)<br /><br /> 弃用|获取正在调试进程的会话的名称。<br /><br /> 弃用. 应始终返回 `E_NOTIMPL` 。]|
|[EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)|枚举进程中运行的线程。|
|[CauseBreak](../../../extensibility/debugger/reference/idebugprocess2-causebreak.md)|请求在此进程中运行代码的下一个程序停止。|
|[GetPort](../../../extensibility/debugger/reference/idebugprocess2-getport.md)|获取运行此进程的端口。|

## <a name="remarks"></a>备注
 `IDebugProcess2`包含一个或多个[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口。

## <a name="requirements"></a>要求
 标头： Msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetProcess](../../../extensibility/debugger/reference/idebugport2-getprocess.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [GetProcess](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)
- [下一页](../../../extensibility/debugger/reference/ienumdebugprocesses2-next.md)
- [事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
