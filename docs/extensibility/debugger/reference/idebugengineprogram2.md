---
title: IDebugEngineProgram2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2
helpviewer_keywords:
- IDebugEngineProgram2 interface
ms.assetid: 151003a9-2e4d-4acf-9f4d-365dfa6b9596
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8e5ccf2327e660a983bcb3032363a92ac8a6f71d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730295"
---
# <a name="idebugengineprogram2"></a>IDebugEngineProgram2
此接口提供多线程调试支持。

## <a name="syntax"></a>语法

```
IDebugEngineProgram2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎实现此接口以支持多个线程的同步调试。 此接口在实现[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口的同一对象上实现。

## <a name="notes-for-callers"></a>呼叫者备注
 使用[查询接口](/cpp/atl/queryinterface)从`IDebugProgram2`接口获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugEngineProgram2`。

|方法|描述|
|------------|-----------------|
|[停止](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)|停止在此程序中运行的所有线程。|
|[WatchForThreadStep](../../../extensibility/debugger/reference/idebugengineprogram2-watchforthreadstep.md)|监视在给定线程上执行（或停止监视执行）。|
|[WatchForExpressionEvaluationOnThread](../../../extensibility/debugger/reference/idebugengineprogram2-watchforexpressionevaluationonthread.md)|允许（或不允许）在给定线程上进行表达式计算，即使程序已停止也是如此。|

## <a name="remarks"></a>备注
 Visual Studio 调用此接口以响应[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件，并设置程序的"线程步骤监视"和"线程表达式评估监视"状态。 每当停止程序时，都会调用"停止";因此，每当程序停止时，都会调用["停止"。](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)此方法使程序有机会终止所有线程。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
