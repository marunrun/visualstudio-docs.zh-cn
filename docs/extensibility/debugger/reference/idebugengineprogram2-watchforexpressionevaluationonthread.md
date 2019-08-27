---
title: IDebugEngineProgram2::WatchForExpressionEvaluationOnThread |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
helpviewer_keywords:
- IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
ms.assetid: 01d05e77-8cac-4d1b-b19f-25756767ed27
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e72292f403b28c66cddbcee623f27ddfcbe5c3aa
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66345181"
---
# <a name="idebugengineprogram2watchforexpressionevaluationonthread"></a>IDebugEngineProgram2::WatchForExpressionEvaluationOnThread
允许 （或不允许） 表达式计算，即使程序已停止，在给定的线程上发生。

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
[in][IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象，表示计算表达式的程序。

`dwTid`\
[in]指定线程的标识符。

`dwEvalFlags`\
[in]中的标志的组合[EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)指定计算的执行方式的枚举。

`pExprCallback`\
[in][IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)要用来发送在表达式计算期间发生的调试事件的对象。

`fWatch`\
[in]如果非零值 (`TRUE`)，由标识的线程上允许表达式评估`dwTid`; 否则为零 (`FALSE`) 不允许该线程上的表达式计算。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 当会话调试管理器 (SDM) 要求的程序，由标识`pOriginatingProgram`参数，以计算表达式，它通过调用此方法将通知所有其他附加的程序。

 在一个程序中的表达式计算可能会导致代码运行在另一个，由于函数求值或任何评估`IDispatch`属性。 因此，此方法允许运行并完成即使线程可能会停止此程序中的表达式计算。

## <a name="see-also"></a>请参阅
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)