---
title: IDebugProgram2：：继续 |微软文档
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
ms.openlocfilehash: 6d04445a7a1c444f30a0ef5c156dcd7ad744c6f1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723074"
---
# <a name="idebugprogram2continue"></a>IDebugProgram2::Continue
继续从已停止状态运行此程序。 保留任何以前的执行状态（如步骤），程序将再次开始执行。

> [!NOTE]
> 不推荐使用此方法。 请改用["继续"](../../../extensibility/debugger/reference/idebugprocess3-continue.md)方法。

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
`pThread`[在]表示线程的[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 无论正在调试的程序数或哪个程序生成停止事件，此程序都会调用此方法。 实现必须保留以前的执行状态（如步骤），并继续执行，就好像在完成之前执行之前从未停止过一样。 也就是说，如果此程序中的线程执行过单操作，并且由于其他程序停止而停止，然后调用此方法，则程序必须完成原始跨行操作。

> [!WARNING]
> 在处理此调用时，不要向[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)发送停止事件或立即（同步）事件;否则调试器可能会挂起。

## <a name="see-also"></a>请参阅
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
