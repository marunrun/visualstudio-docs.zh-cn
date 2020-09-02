---
title: IDebugProcess3：： Continue |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Continue
helpviewer_keywords:
- IDebugProcess3::Continue
ms.assetid: 57506242-5763-4c08-adb9-8a78ce02cebb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: aba0863ad7c50bf5c14e7a30c06097825b8cf5ec
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86386792"
---
# <a name="idebugprocess3continue"></a>IDebugProcess3::Continue
继续从停止状态运行此进程。 任何以前的执行状态 (例如步骤) 会保留，该进程将再次开始执行。

> [!NOTE]
> 应使用此方法，而不是 [继续](../../../extensibility/debugger/reference/idebugprogram2-continue.md)。

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
`pThread`\
中表示要继续的线程的 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 无论正在调试多少进程，或哪个进程生成了停止事件，都将在此过程中调用此方法。 实现必须保留以前的执行状态 (例如步骤) 并继续执行，就像在完成前一次执行之前从未停止过。 也就是说，如果此进程中的线程正在执行逐过程操作，并且由于其他进程停止，然后 `Continue` 调用，则指定线程必须完成原始的逐步骤操作。

 **警告** 处理此调用时，不要将停止事件或立即 (同步) 事件发送到 [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) ;否则，调试器可能会停止响应。

## <a name="see-also"></a>另请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
