---
title: IDebugEngineProgram2：：观看表达式评估线程 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
helpviewer_keywords:
- IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
ms.assetid: 01d05e77-8cac-4d1b-b19f-25756767ed27
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e988e1d64af38a55f5d946f704e1edb4df29b1d5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730362"
---
# <a name="idebugengineprogram2watchforexpressionevaluationonthread"></a>IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
允许（或不允许）在给定线程上进行表达式计算，即使程序已停止也是如此。

## <a name="syntax"></a>语法

```cpp
HRESULT WatchForExpressionEvaluationOnThread( 
   IDebugProgram2*       pOriginatingProgram,
   DWORD                 dwTid,
   DWORD                 dwEvalFlags,
   IDebugEventCallback2* pExprCallback,
   BOOL                  fWatch
);
```

```csharp
int WatchForExpressionEvaluationOnThread( 
   IDebugProgram2       pOriginatingProgram,
   uint                  dwTid,
   uint                  dwEvalFlags,
   IDebugEventCallback2 pExprCallback,
   int                   fWatch
);
```

## <a name="parameters"></a>参数
`pOriginatingProgram`\
[在][IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象，表示正在评估表达式的程序。

`dwTid`\
[在]指定线程的标识符。

`dwEvalFlags`\
[在][EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)枚举中的标志组合，用于指定如何执行计算。

`pExprCallback`\
[在]用于发送表达式计算期间发生的调试事件的[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)对象。

`fWatch`\
[在]如果非零 （），`TRUE`允许在 标识的`dwTid`线程上进行表达式计算。否则，零`FALSE`（ ） 不允许对该线程的表达式计算。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 当会话调试管理器 （SDM） 要求`pOriginatingProgram`由参数标识的程序评估表达式时，它会通过调用此方法通知所有其他附加的程序。

 由于函数计算或任何`IDispatch`属性的评估，一个程序中的表达式计算可能会导致代码在另一个程序中运行。 因此，此方法允许表达式计算运行和完成，即使线程可能在此程序中停止。

## <a name="see-also"></a>请参阅
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
