---
title: IDebugProgramDestroyEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramDestroyEvent2
helpviewer_keywords:
- IDebugProgramDestroyEvent2
ms.assetid: ddf127ca-c4a5-4071-90ca-68faf2f57dbd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dd9f7b97dc7479b90801ebcd07966a0058fa6476
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66343543"
---
# <a name="idebugprogramdestroyevent2"></a>IDebugProgramDestroyEvent2
当程序已完成运行时，此接口是由调试引擎 (DE) 发送到会话调试管理器 (SDM) 中。

## <a name="syntax"></a>语法

```
IDebugProgramDestroyEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 DE 或自定义端口供应商实现报告程序已终止，并且不再可用于调试此接口。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象。 使用 SDM [QueryInterface](/cpp/atl/queryinterface)访问`IDebugEvent2`接口。

## <a name="notes-for-callers"></a>调用方的说明
 DE 或自定义端口供应商创建并发送报告的程序终止此事件对象。 DE 发送该事件通过使用[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 它附加到正在调试的程序时提供的回调函数。 自定义端口供应商发送此事件使用[IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugProgramDestroyEvent2`。

|方法|描述|
|------------|-----------------|
|[GetExitCode](../../../extensibility/debugger/reference/idebugprogramdestroyevent2-getexitcode.md)|获取该程序的退出代码。|

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)