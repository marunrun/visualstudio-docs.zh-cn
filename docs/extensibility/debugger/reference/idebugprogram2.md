---
title: IDebugProgram2 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722717"
---
# <a name="idebugprogram2"></a>IDebugProgram2
此接口表示进程中运行的程序。

## <a name="syntax"></a>语法

```
IDebugProgram2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 和自定义端口供应商实现此接口以表示进程中的程序。 会话调试管理器 （SDM） 还实现此接口，以向[附加](../../../extensibility/debugger/reference/idebugprogram2-attach.md)提供信息。

## <a name="notes-for-callers"></a>呼叫者备注
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件返回新程序的此接口。 此接口还用作多个接口上许多方法的参数。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugProgram2`。

|方法|描述|
|------------|-----------------|
|[EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)|枚举此程序中运行的线程。|
|[GetName](../../../extensibility/debugger/reference/idebugprogram2-getname.md)|获取程序的名称。|
|[获取过程](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)|获取此程序正在运行的进程。|
|[终止](../../../extensibility/debugger/reference/idebugprogram2-terminate.md)|终止此程序。|
|[Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md)|附加到此程序。|
|[CanDetach](../../../extensibility/debugger/reference/idebugprogram2-candetach.md)|确定调试引擎 （DE） 是否可以从程序分离。|
|[Detach](../../../extensibility/debugger/reference/idebugprogram2-detach.md)|从该程序分离调试器。|
|[GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)|获取此程序的全局唯一标识符。|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md)|获取程序属性。|
|[执行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)|继续从已停止状态运行此程序。 清除任何以前的执行状态。|
|[继续](../../../extensibility/debugger/reference/idebugprogram2-continue.md)|继续从已停止状态运行此程序。 保留任何以前的执行状态。|
|[步骤](../../../extensibility/debugger/reference/idebugprogram2-step.md)|执行步骤。|
|[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)|请求下次其线程运行代码时停止执行此程序。|
|[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)|获取运行此程序的调试引擎 （DE） 的名称和标识符。|
|[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)|枚举源文件中给定位置的代码上下文。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)|获取此程序的内存字节。|
|[GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)|获取此程序或此程序的一部分的拆解流。|
|[EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)|枚举此程序已加载并正在执行的模块。|
|[GetENCUpdate](../../../extensibility/debugger/reference/idebugprogram2-getencupdate.md)|获取此程序的编辑和继续 （ENC） 更新。<br /><br /> 自定义调试引擎不实现此方法（应始终返回`E_NOTIMPL`）。|
|[EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md)|枚举此程序的代码路径。|
|[WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)|将转储写入文件。|

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="remarks"></a>备注
 程序是在特定的运行时体系结构中运行的线程容器，而进程由一个或多个程序组成。

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)
- [下一步](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)
- [事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
