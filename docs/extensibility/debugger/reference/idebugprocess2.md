---
title: IDebugProcess2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2
helpviewer_keywords:
- IDebugProcess2 interface
ms.assetid: 99f6cd06-4076-45ee-b2ae-fa2ad627fd18
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0bea73c1bce5367d9686e835bb58dd99a83cc818
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66314129"
---
# <a name="idebugprocess2"></a>IDebugProcess2
此接口表示的端口上运行的进程。 如果端口为本地端口，则`IDebugProcess2`通常表示本地计算机上的物理进程。

## <a name="syntax"></a>语法

```
IDebugProcess2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 此接口由自定义端口提供程序作为一个组管理程序实现。 此接口必须由端口提供程序实现。

 调试引擎还实现此接口，如果它支持启动程序通过[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)。

## <a name="notes-for-callers"></a>调用方的说明
 此接口称为主要由会话调试管理器 (SDM) 以便与一组在此过程中标识的程序进行交互。

 调用[GetProcess](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)或[GetProcess](../../../extensibility/debugger/reference/idebugport2-getprocess.md)来获得此接口。 此接口也会返回通过调用`IDebugEngineLaunch2::LaunchSuspended`。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugProcess2`。

|方法|描述|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)|获取过程的说明。|
|[EnumPrograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)|枚举包含在此过程中的程序。|
|[GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)|获取标题、 友好名称或进程的文件名称。|
|[GetServer](../../../extensibility/debugger/reference/idebugprocess2-getserver.md)|获取计算机服务器运行此过程的实例。|
|[Terminate](../../../extensibility/debugger/reference/idebugprocess2-terminate.md)|终止进程。|
|[附加](../../../extensibility/debugger/reference/idebugprocess2-attach.md)|附加到进程。|
|[CanDetach](../../../extensibility/debugger/reference/idebugprocess2-candetach.md)|确定 SDM 可以与进程分离。|
|[分离](../../../extensibility/debugger/reference/idebugprocess2-detach.md)|将调试器与进程分离。|
|[GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)|获取系统进程标识符。|
|[GetProcessId](../../../extensibility/debugger/reference/idebugprocess2-getprocessid.md)|获取此进程的全局唯一标识符。|
|[GetAttachedSessionName](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)<br /><br /> [弃用]|获取正在调试的进程的会话的名称。<br /><br /> [已弃用。 应始终返回`E_NOTIMPL`。]|
|[EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)|枚举的进程中运行的线程。|
|[CauseBreak](../../../extensibility/debugger/reference/idebugprocess2-causebreak.md)|将请求中此进程停止运行代码的下一步程序。|
|[GetPort](../../../extensibility/debugger/reference/idebugprocess2-getport.md)|获取此进程运行的端口。|

## <a name="remarks"></a>备注
 `IDebugProcess2`包含一个或多个[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口。

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetProcess](../../../extensibility/debugger/reference/idebugport2-getprocess.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [GetProcess](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)
- [下一页](../../../extensibility/debugger/reference/ienumdebugprocesses2-next.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)