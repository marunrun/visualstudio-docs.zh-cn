---
title: IDebug表达式上下文2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionContext2
helpviewer_keywords:
- IDebugExpressionContext2 interface
ms.assetid: 577fdaae-4b2d-4112-9839-ab899535fa6f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 344ae287b3784ceca87fbbab09ad2b2e0a304205
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729637"
---
# <a name="idebugexpressioncontext2"></a>IDebugExpressionContext2
此接口表示表达式计算的上下文

## <a name="syntax"></a>语法

```
IDebugExpressionContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口以表示可以计算表达式的上下文。

## <a name="notes-for-callers"></a>呼叫者备注
 对[GetExpressionContext 的](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)调用将返回此接口。 仅当正在调试的程序已暂停且堆栈帧可用时，才能访问此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugExpressionContext2`。

|方法|描述|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugexpressioncontext2-getname.md)|检索评估上下文的名称。|
|[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)|分析用于计算的基于文本的表达式。|

## <a name="remarks"></a>备注
 可以将评估上下文视为执行表达式计算的范围。

 当程序停止时，会话调试管理器 （SDM） 从 DE 获取一个堆栈帧，并调用[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)。 然后，SDM 调用[GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) `IDebugExpressionContext2`来获取接口。 然后调用[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)以创建[IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)接口，该接口表示可供计算的解析表达式。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
