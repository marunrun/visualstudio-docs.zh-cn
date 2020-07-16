---
title: IDebugProgram2：： Continue |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Continue
helpviewer_keywords:
- IDebugProgram2::Continue
ms.assetid: e5a6e02a-d21b-4a03-a034-e8de1f71ce2e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ee73ea3a9b65635cf14d4d345bf22de4e9593989
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2020
ms.locfileid: "86387078"
---
# <a name="idebugprogram2continue"></a>IDebugProgram2::Continue
继续从停止状态运行该程序。 任何以前的执行状态（如步骤）都将被保留，程序将重新开始执行。

> [!NOTE]
> 不推荐使用此方法。 请改用[Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md)方法。

## <a name="syntax"></a>语法

```cpp
HRESULT Continue( 
   IDebugThread2* pThread
);
```

```csharp
int Continue( 
   IDebugThread2 pThread
);
```

## <a name="parameters"></a>参数
`pThread`中表示线程的[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 无论正在调试的程序有多少，或哪个程序生成了停止事件，都将对此程序调用此方法。 实现必须保留以前的执行状态（如步骤），并继续执行，就像在完成前一次执行之前从未停止。 也就是说，如果此程序中的某个线程执行了逐过程操作，并且由于其他程序停止而停止，然后调用此方法，则该程序必须完成原始的逐步骤操作。

> [!WARNING]
> 处理此调用时，不要将停止事件或即时（同步）事件发送到[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md);否则，调试器可能会停止响应。

## <a name="see-also"></a>另请参阅
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
