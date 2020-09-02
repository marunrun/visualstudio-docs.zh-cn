---
title: IDebugExpressionEvaluationCompleteEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluationCompleteEvent2
helpviewer_keywords:
- IDebugExpressionEvaluationCompleteEvent2
ms.assetid: d538fc19-55bf-4231-9595-eb01e84fd1d8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 35e57e361b59e76e187617b5e528b219e8e47897
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80729556"
---
# <a name="idebugexpressionevaluationcompleteevent2"></a>IDebugExpressionEvaluationCompleteEvent2
当异步表达式计算完成时，调试引擎会将此接口 (DE) 发送到会话调试管理器 (SDM) 。

## <a name="syntax"></a>语法

```
IDebugExpressionEvaluationCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 DE 实现此接口，报告通过调用 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)启动表达式计算的完成。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 [QueryInterface](/cpp/atl/queryinterface) 访问 `IDebugEvent2` 接口。

## <a name="notes-for-callers"></a>调用方说明
 DE 创建并发送此事件对象，以报告表达式计算的完成。 使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送事件。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugExpressionEvaluationCompleteEvent2` 。

|方法|说明|
|------------|-----------------|
|[GetExpression](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)|获取原始表达式。|
|[GetResult](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)|获取表达式计算的结果。|

## <a name="remarks"></a>备注
 DE 必须发送此事件，计算是否成功。

 如果计算不成功，则不会 `DEBUG_PROPINFO_VALUE` `DEBUG_PROPINFO_ATTRIB` 在 GetPropertyInfo 返回的[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构中设置和标志， [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)对象由 ([GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)创建， `IDebugExpressionEvaluationCompleteEvent2` 如果计算失败) ，则在事件中返回。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
