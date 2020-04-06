---
title: IDebugProcess2 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723797"
---
# <a name="idebugprocess2"></a>IDebugProcess2
此接口表示在端口上运行的进程。 如果端口是本地端口，则`IDebugProcess2`通常表示本地计算机上的物理进程。

## <a name="syntax"></a>语法

```
IDebugProcess2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 此接口由自定义端口供应商实现，以作为一个组管理程序。 此接口必须由端口供应商实现。

 如果调试引擎支持通过[Launch暂停](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)启动程序，则调试引擎也将实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
 此接口主要由会话调试管理器 （SDM） 调用，以便与在此过程中标识的一组程序进行交互。

 调用[GetProcess](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)或[GetProcess](../../../extensibility/debugger/reference/idebugport2-getprocess.md)获取此接口。 此接口也通过调用`IDebugEngineLaunch2::LaunchSuspended`返回。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugProcess2`。

|方法|描述|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)|获取流程的说明。|
|[EnumPrograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)|枚举此过程中包含的程序。|
|[GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)|获取进程的标题、友好名称或文件名。|
|[GetServer](../../../extensibility/debugger/reference/idebugprocess2-getserver.md)|获取此进程运行的计算机服务器的实例。|
|[终止](../../../extensibility/debugger/reference/idebugprocess2-terminate.md)|终止进程。|
|[Attach](../../../extensibility/debugger/reference/idebugprocess2-attach.md)|附加到进程。|
|[CanDetach](../../../extensibility/debugger/reference/idebugprocess2-candetach.md)|确定 SDM 是否可以分离进程。|
|[Detach](../../../extensibility/debugger/reference/idebugprocess2-detach.md)|从进程分离调试器。|
|[GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)|获取系统进程标识符。|
|[获取进程 Id](../../../extensibility/debugger/reference/idebugprocess2-getprocessid.md)|获取此过程的全局唯一标识符。|
|[GetAttachedSessionName](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)<br /><br /> [已弃用]|获取调试进程的会话的名称。<br /><br /> *已弃用。 应始终返回`E_NOTIMPL`。|
|[EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)|枚举进程中运行的线程。|
|[CauseBreak](../../../extensibility/debugger/reference/idebugprocess2-causebreak.md)|请求进程中运行代码的下一个程序停止。|
|[GetPort](../../../extensibility/debugger/reference/idebugprocess2-getport.md)|获取此进程正在运行的端口。|

## <a name="remarks"></a>备注
 包含`IDebugProcess2`一个或多个[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口。

## <a name="requirements"></a>要求
 标题： Msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [获取过程](../../../extensibility/debugger/reference/idebugport2-getprocess.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [获取过程](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)
- [下一步](../../../extensibility/debugger/reference/ienumdebugprocesses2-next.md)
- [事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
