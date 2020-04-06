---
title: IDebugProgram3 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgram3 interface
ms.assetid: 4301ba23-c00c-4ce5-8b1e-3f27da312034
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9da63d54f64a4ef7592fdbc4d36e2b31220f82df
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722641"
---
# <a name="idebugprogram3"></a>IDebugProgram3
此接口表示在进程中运行的程序，并通过提供线程信息扩展[Execute。](../../../extensibility/debugger/reference/idebugprogram2-execute.md)

## <a name="syntax"></a>语法

```
IDebugProgram3 : IDebugProgram3
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 和自定义端口供应商实现此接口以表示进程中的程序。 会话调试管理器 （SDM） 还实现此接口，以向[附加](../../../extensibility/debugger/reference/idebugprogram2-attach.md)提供信息。

## <a name="notes-for-callers"></a>呼叫者备注
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件返回新程序的此接口。 此接口还用作多个接口上许多方法的参数。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugProgram3`。

|方法|描述|
|------------|-----------------|
|[ExecuteOnThread](../../../extensibility/debugger/reference/idebugprogram3-executeonthread.md)|执行程序。 返回线程以向调试器提供有关用户在执行时正在查看的线程的信息。|

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="remarks"></a>备注
 程序是在特定的运行时体系结构中运行的线程容器，而进程由一个或多个程序组成。

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)
- [下一步](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)
- [事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
