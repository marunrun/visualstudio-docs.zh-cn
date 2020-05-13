---
title: IDebugEngineLaunch2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineLaunch2
helpviewer_keywords:
- IDebugEngineLaunch2 interface
ms.assetid: 5eaf2ad8-3fbf-446e-b48b-5327ad3f5255
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ee77cbd680df2c851d53aac298605023227fa6f8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730493"
---
# <a name="idebugenginelaunch2"></a>IDebugEngineLaunch2
调试引擎 （DE） 用于启动和终止程序。

## <a name="syntax"></a>语法

```
IDebugEngineLaunch2 : IDebugEngine2
```

## <a name="notes-for-implementers"></a>实施者说明
 如果此接口具有启动不能完全由自定义端口处理的进程的特殊要求，则此接口由自定义 DE 实现。 当 DE 是解释器的一部分，并且正在调试的过程是一个脚本时，通常就是这种情况：首先需要启动解释器，然后加载和启动脚本。 端口可以启动解释器，但脚本可能需要特殊处理（这是 DE 具有角色的位置）。 仅当存在启动自定义端口无法处理的程序的唯一要求时，才会实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
 如果 SDM 可以从[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)接口（使用查询接口）获取此接口，会话调试管理器 （SDM） 会调用此接口。 如果可以获取此接口，SDM 知道 DE 具有特殊要求，并调用此接口启动程序，而不是让端口启动它。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugEngineLaunch2`。

|方法|描述|
|------------|-----------------|
|[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)|通过 DE 启动进程。|
|[ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)|恢复进程执行。|
|[CanTerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-canterminateprocess.md)|确定是否可以终止进程。|
|[TerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-terminateprocess.md)|终止进程。|

## <a name="requirements"></a>要求
 标题： Msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
