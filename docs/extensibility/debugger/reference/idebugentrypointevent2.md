---
title: IDebugEntryPointEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEntryPointEvent2
helpviewer_keywords:
- IDebugEntryPointEvent2 interface
ms.assetid: a15d1cc3-97b7-438c-8d24-c23149708f42
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5c2cd0f92e5bd954c8247fa86c39f3ad206aa99b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66345102"
---
# <a name="idebugentrypointevent2"></a>IDebugEntryPointEvent2
当程序要执行其第一个指令的用户代码时，调试引擎 (DE) 会将此接口发送到会话调试管理器 (SDM)。

## <a name="syntax"></a>语法

```
IDebugEntryPointEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 DE 实现此接口作为其常规操作的一部分。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象。 使用 SDM [QueryInterface](/cpp/atl/queryinterface)访问`IDebugEvent2`接口。

## <a name="notes-for-callers"></a>调用方的说明
 DE 创建并发送此事件对象，当正在调试的程序已加载并已准备好执行用户代码的第一个指令。 通过使用发送该事件[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 它附加到正在调试的程序时提供的回调函数。

## <a name="remarks"></a>备注
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)程序即将执行的第一个指令时发送。 例如，`IDebugEntryPoint2`时该程序将要执行的用户发送`main`函数。

 当发送 DE `IDebugEntryPointEvent2`，当前的代码位置应为在用户代码的第一个指令如`main`。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)