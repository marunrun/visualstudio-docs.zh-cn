---
title: IDebugEngineProgram2：： Stop |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::Stop
helpviewer_keywords:
- IDebugEngineProgram2::Stop
ms.assetid: 6e1c3d56-fb67-4a5b-80f9-8ee5131972bf
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9d7213dcd2484ba69caf51fdc21f52bba5bb3361
ms.sourcegitcommit: 260d093d2287ba791f28bdc7103493beabf80b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77506446"
---
# <a name="idebugengineprogram2stop"></a>IDebugEngineProgram2::Stop
停止在此程序中运行的所有线程。

## <a name="syntax"></a>语法

```cpp
HRESULT Stop( 
   void 
);
```

```csharp
int Stop();
```

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 在多程序环境中调试此程序时，将调用此方法。 当收到来自某个其他程序的停止事件时，将对此程序调用此方法。 此方法的实现应为异步;也就是说，在此方法返回之前，并不是所有线程都需要停止。 此方法的实现可能与在此程序上调用[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)方法一样简单。

 当程序停止时，实现程序应发送[IDebugStopCompleteEvent2](../../../extensibility/debugger/reference/idebugstopcompleteevent2.md) 。

## <a name="see-also"></a>另请参阅
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
