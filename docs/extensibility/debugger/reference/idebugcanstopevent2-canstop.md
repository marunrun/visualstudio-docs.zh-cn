---
title: IDebugcanStopevent2：：：可以停止 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::CanStop
helpviewer_keywords:
- IDebugCanStopEvent2::CanStop
ms.assetid: 7d61adbe-6b3d-41f3-86a1-45d9cc01a7f8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2915938c966bac7f842d0745c973c7d0b7033e2b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734590"
---
# <a name="idebugcanstopevent2canstop"></a>IDebugCanStopEvent2::CanStop
通知调试引擎 （DE） 是否停止在当前代码位置或只是继续执行。

## <a name="syntax"></a>语法

```cpp
HRESULT CanStop ( 
   BOOL fCanStop
);
```

```csharp
int CanStop ( 
   int fCanStop
);
```

## <a name="parameters"></a>参数
`fCanStop`\
[在]如果 DE`TRUE`应停止在当前代码位置，则非零 （ ） ;否则，零`FALSE`（）。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 此事件的接收方通常调用[GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)方法以确定 DE 想要停止的原因，然后使用适当的响应调用`IDebugCanStopEvent2::CanStop`该方法。

 如果 DE 停止，它将发送描述停止原因的事件。 通常发送两个事件，一个由[IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)接口表示的用户或信号中断，以及[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)接口表示的断点事件。

## <a name="see-also"></a>请参阅
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)
- [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)
- [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)
