---
title: IDebugProgramCreateEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramCreateEvent2
helpviewer_keywords:
- IDebugProgramCreateEvent2 interface
ms.assetid: b19a7934-6179-4a68-9075-bd7dcd640b05
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8081e05d18719af060ddf58045c06ec64036ae35
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331454"
---
# <a name="idebugprogramcreateevent2"></a>IDebugProgramCreateEvent2
程序附加到时，此接口是由调试引擎 (DE) 发送到会话调试管理器 (SDM) 中。

## <a name="syntax"></a>语法

```
IDebugProgramCreateEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 DE 或自定义端口提供程序实现此接口可报告的程序创建后，通常在程序附加到的时间。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象。 使用 SDM`QueryInterface`方法访问`IDebugEvent2`接口。

## <a name="notes-for-callers"></a>调用方的说明
 DE 或自定义端口供应商创建并发送此事件对象来报告创建一个计划。 DE 发送该事件通过使用[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 它附加到正在调试的程序时提供的回调函数。 自定义端口供应商发送此事件使用[IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)接口。

## <a name="remarks"></a>备注
 DE 或自定义端口供应商发布的新[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)接口通过调用[PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)