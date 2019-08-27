---
title: IDebugEngineProgram2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2
helpviewer_keywords:
- IDebugEngineProgram2 interface
ms.assetid: 151003a9-2e4d-4acf-9f4d-365dfa6b9596
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 221ab8fd00bc7d98745fdd5cc03dd72b9919b4b2
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66345141"
---
# <a name="idebugengineprogram2"></a>IDebugEngineProgram2
此接口提供了多线程调试支持。

## <a name="syntax"></a>语法

```
IDebugEngineProgram2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎实现此接口以支持多个线程的同时进行调试。 此接口上实现的相同对象实现[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口。

## <a name="notes-for-callers"></a>调用方的说明
 使用[QueryInterface](/cpp/atl/queryinterface)若要获取此接口从`IDebugProgram2`接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugEngineProgram2`。

|方法|描述|
|------------|-----------------|
|[Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)|停止此程序中正在运行的所有线程。|
|[WatchForThreadStep](../../../extensibility/debugger/reference/idebugengineprogram2-watchforthreadstep.md)|执行 （或停止执行监视） 监视是否在给定的线程上发生。|
|[WatchForExpressionEvaluationOnThread](../../../extensibility/debugger/reference/idebugengineprogram2-watchforexpressionevaluationonthread.md)|允许 （或不允许） 表达式计算，即使程序已停止，在给定的线程上发生。|

## <a name="remarks"></a>备注
 Visual Studio 会调用此接口以响应[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件并设置该程序的"监视的线程步骤"和"监视的表达式求值在线程"状态。 [停止](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)每当调用程序是要停止; 此方法使程序终止所有线程。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)