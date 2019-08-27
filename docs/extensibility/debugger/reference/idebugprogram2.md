---
title: IDebugProgram2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2
helpviewer_keywords:
- IDebugProgram2 interface
ms.assetid: 8d73df73-cfff-4b8b-b426-d6051edb1939
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5c79ec83adcb766bd7c6de3d31a2ae790710a838
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348953"
---
# <a name="idebugprogram2"></a>IDebugProgram2
此接口表示进程中运行的程序。

## <a name="syntax"></a>语法

```
IDebugProgram2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎 (DE) 和自定义端口提供程序实现此接口来表示在进程中的程序。 会话调试管理器 (SDM) 也实现此接口将信息提供给[附加](../../../extensibility/debugger/reference/idebugprogram2-attach.md)。

## <a name="notes-for-callers"></a>调用方的说明
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件返回此接口的新程序。 此接口还用作多个接口上的许多方法参数。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugProgram2`。

|方法|描述|
|------------|-----------------|
|[EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)|枚举在此程序中运行的线程。|
|[GetName](../../../extensibility/debugger/reference/idebugprogram2-getname.md)|获取该程序的名称。|
|[GetProcess](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)|获取此程序在运行时的进程。|
|[Terminate](../../../extensibility/debugger/reference/idebugprogram2-terminate.md)|终止此程序。|
|[附加](../../../extensibility/debugger/reference/idebugprogram2-attach.md)|将附加到此程序。|
|[CanDetach](../../../extensibility/debugger/reference/idebugprogram2-candetach.md)|确定是否调试引擎 (DE) 可以从程序分离。|
|[分离](../../../extensibility/debugger/reference/idebugprogram2-detach.md)|分离调试程序与此程序。|
|[GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)|获取此程序的全局唯一标识符。|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md)|获取程序属性。|
|[Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md)|将继续运行此程序从已停止状态。 清除任何以前的执行状态。|
|[Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md)|将继续运行此程序从已停止状态。 保留任何以前的执行状态。|
|[Step](../../../extensibility/debugger/reference/idebugprogram2-step.md)|执行一个步骤。|
|[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)|此程序停止执行下一个请求时间 1 其线程运行代码。|
|[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)|获取名称和运行此程序的调试引擎 (DE) 的标识符。|
|[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)|枚举在源文件中的给定位置的代码上下文。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)|获取此程序的内存字节数。|
|[GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)|获取此程序或此计划的一部分的反汇编流。|
|[EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)|枚举此程序已加载且正在执行的模块。|
|[GetENCUpdate](../../../extensibility/debugger/reference/idebugprogram2-getencupdate.md)|获取此程序编辑并继续 (ENC) 更新。<br /><br /> 自定义调试引擎不实现此方法 (它应始终返回`E_NOTIMPL`)。|
|[EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md)|枚举此程序的代码路径。|
|[WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)|将转储写入到一个文件。|

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>备注
 程序是运行在特定的运行时体系结构中，而进程组成一个或多个程序的线程容器。

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)
- [下一页](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)