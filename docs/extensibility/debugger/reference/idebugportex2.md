---
title: IDebugPortEx2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEx2
helpviewer_keywords:
- IDebugPortEx2 interface
ms.assetid: 144724d0-38ee-4c9b-87ca-8a504371182b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5789681b0da70f46dadac1e29d0d6bb9dc905d1a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724997"
---
# <a name="idebugportex2"></a>IDebugPortEx2
此接口允许会话调试管理器 （SDM） 控制在端口上运行的程序和进程。

## <a name="syntax"></a>语法

```
IDebugPortEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 自定义端口供应商在实现[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)的同一对象上实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
 SDM 在接口上`IDebugPort2`调用[查询接口](/cpp/atl/queryinterface)以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugPortEx2`。

|方法|描述|
|------------|-----------------|
|[LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)|启动可执行文件。|
|[ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md)|恢复进程的执行。|
|[CanTerminateProcess](../../../extensibility/debugger/reference/idebugportex2-canterminateprocess.md)|确定是否可以终止进程。|
|[TerminateProcess](../../../extensibility/debugger/reference/idebugportex2-terminateprocess.md)|终止进程。|
|[GetPortProcessId](../../../extensibility/debugger/reference/idebugportex2-getportprocessid.md)|获取端口本身的进程 ID。|
|[GetProgram](../../../extensibility/debugger/reference/idebugportex2-getprogram.md)|获取与程序节点关联的程序。|

## <a name="remarks"></a>备注
 此接口通常是 SDM 和自定义端口供应商之间的私有接口。

 如果需要，调试引擎 （DE） 可以在[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)接口上查找此接口，该接口传递给[Launch暂停](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)，并使用[Launch暂停](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)启动程序。 但是，这不是要求，DE 可以执行启动请求程序所需的任何操作。

## <a name="requirements"></a>要求
 标题： portpriv.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
