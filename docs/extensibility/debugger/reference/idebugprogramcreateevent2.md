---
title: IDebugProgram创建事件2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramCreateEvent2
helpviewer_keywords:
- IDebugProgramCreateEvent2 interface
ms.assetid: b19a7934-6179-4a68-9075-bd7dcd640b05
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 78088d6e5da61c32302c13b08143c9ed902452e2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722626"
---
# <a name="idebugprogramcreateevent2"></a>IDebugProgramCreateEvent2
此接口由调试引擎 （DE） 连接到会话调试管理器 （SDM） 时发送到会话调试管理器 （SDM）。

## <a name="syntax"></a>语法

```
IDebugProgramCreateEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 DE 或自定义端口供应商实现此接口以报告已创建程序（通常在程序附加到程序时）。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现。 SDM 使用`QueryInterface`方法访问`IDebugEvent2`接口。

## <a name="notes-for-callers"></a>呼叫者备注
 DE 或自定义端口供应商创建并发送此事件对象以报告程序的创建。 DE 使用 SDM 在连接到正在调试的程序时提供的[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)回调函数发送此事件。 自定义端口供应商使用[IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)接口发送此事件。

## <a name="remarks"></a>备注
 DE 或自定义端口供应商通过调用[PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)发布新的[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)接口。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
