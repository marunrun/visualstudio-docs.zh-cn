---
title: IDebugExpressionEvaluationCompleteEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluationCompleteEvent2
helpviewer_keywords:
- IDebugExpressionEvaluationCompleteEvent2
ms.assetid: d538fc19-55bf-4231-9595-eb01e84fd1d8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5af187e04096fdd16dc5a371f49953fae2e61621
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66325732"
---
# <a name="idebugexpressionevaluationcompleteevent2"></a>IDebugExpressionEvaluationCompleteEvent2
完成异步表达式求值时，此接口是由调试引擎 (DE) 发送到会话调试管理器 (SDM) 中。

## <a name="syntax"></a>语法

```
IDebugExpressionEvaluationCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 DE 实现此接口以通过调用启动表达式计算的报表完成[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象。 使用 SDM [QueryInterface](/cpp/atl/queryinterface)访问`IDebugEvent2`接口。

## <a name="notes-for-callers"></a>调用方的说明
 DE 创建并发送此事件对象来报告已完成表达式计算。 通过使用发送该事件[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 它附加到正在调试的程序时提供的回调函数。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugExpressionEvaluationCompleteEvent2`。

|方法|描述|
|------------|-----------------|
|[GetExpression](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)|获取原始表达式。|
|[GetResult](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)|获取表达式计算的结果。|

## <a name="remarks"></a>备注
 DE 必须发送此事件是否评估是成功还是失败。

 如果计算不成功，`DEBUG_PROPINFO_VALUE`并`DEBUG_PROPINFO_ATTRIB`将不会设置标志[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)返回的结构[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) ( [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) DE 创建并返回在对象`IDebugExpressionEvaluationCompleteEvent2`如果评估失败的事件)。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)