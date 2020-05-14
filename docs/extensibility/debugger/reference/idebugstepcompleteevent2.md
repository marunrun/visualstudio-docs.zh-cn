---
title: IDebugStep完成事件2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStepCompleteEvent2
helpviewer_keywords:
- IDebugStepCompleteEvent2 interface
ms.assetid: eba2b76e-f90d-486b-ae5c-c47f1b8ba2e5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 289609c93cf0e58eb44500bff135282d01212bbc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719459"
---
# <a name="idebugstepcompleteevent2"></a>IDebugStepCompleteEvent2
当正在调试的程序完成一个步骤、一步一步或一步从源代码或语句或指令中完成时，此接口由调试引擎 （DE） 发送到会话调试管理器 （SDM）。

## <a name="syntax"></a>语法

```
IDebugStepCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 DE 实现此接口以报告步骤操作的完成。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现。 SDM 使用[查询接口](/cpp/atl/queryinterface)访问`IDebugEvent2`接口。

## <a name="notes-for-callers"></a>呼叫者备注
 DE 创建并发送此事件对象以报告步骤操作的完成。 该事件使用 SDM 在附加到正在调试的程序时提供的[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)回调函数进行发送。

## <a name="remarks"></a>备注
 步骤完成后，正在调试的程序将再次暂停，IDE 将更新其所有窗口。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
