---
title: IDebugProgram2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2
helpviewer_keywords:
- IDebugProgram2 interface
ms.assetid: 8d73df73-cfff-4b8b-b426-d6051edb1939
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 150746197be4945b012717bef08e18ea57168177
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80722717"
---
# <a name="idebugprogram2"></a>IDebugProgram2
此接口表示在进程中运行的程序。

## <a name="syntax"></a>语法

```
IDebugProgram2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 调试引擎 (DE) ，自定义端口供应商实现此接口来表示进程中的程序。 会话调试管理器 (SDM) 还实现此接口以提供要 [附加](../../../extensibility/debugger/reference/idebugprogram2-attach.md)的信息。

## <a name="notes-for-callers"></a>调用方说明
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件将为新程序返回此接口。 此接口还可用作多个接口上许多方法的参数。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugProgram2` 。

|方法|说明|
|------------|-----------------|
|[EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)|枚举在此程序中运行的线程。|
|[GetName](../../../extensibility/debugger/reference/idebugprogram2-getname.md)|获取程序的名称。|
|[GetProcess](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)|获取此程序在其中运行的进程。|
|Terminate|终止此程序。|
|[附加](../../../extensibility/debugger/reference/idebugprogram2-attach.md)|附加到此程序。|
|[CanDetach](../../../extensibility/debugger/reference/idebugprogram2-candetach.md)|确定调试引擎 (DE) 是否可以与程序分离。|
|[分离](../../../extensibility/debugger/reference/idebugprogram2-detach.md)|从此程序分离调试器。|
|[GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)|获取此程序的全局唯一标识符。|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md)|获取程序属性。|
|[执行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)|继续从停止状态运行该程序。 任何以前的执行状态都将被清除。|
|[继续](../../../extensibility/debugger/reference/idebugprogram2-continue.md)|继续从停止状态运行该程序。 保留以前的执行状态。|
|[步骤](../../../extensibility/debugger/reference/idebugprogram2-step.md)|执行步骤。|
|[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)|请求此程序在下一次运行代码时停止执行。|
|[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)|获取运行此程序)  (DE 调试引擎的名称和标识符。|
|[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)|枚举源文件中给定位置的代码上下文。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)|获取此程序的内存字节数。|
|[GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)|获取此程序或此程序的一部分的反汇编流。|
|[EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)|枚举此程序已加载且正在执行的模块。|
|[GetENCUpdate](../../../extensibility/debugger/reference/idebugprogram2-getencupdate.md)|获取此程序的 "编辑并继续" (ENC) update。<br /><br /> 自定义调试引擎不实现此方法 (应始终返回 `E_NOTIMPL`) 。|
|[EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md)|枚举此程序的代码路径。|
|[WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)|向文件写入转储。|

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>备注
 程序是在特定运行时结构中运行的线程容器，而进程由一个或多个程序组成。

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)
- [下一页](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)
- [事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
