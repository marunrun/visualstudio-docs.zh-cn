---
title: IDebugProcess3：：继续 |微软文档
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
ms.openlocfilehash: f8fa2e21e31297279a173c9c9edd087adc560903
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723777"
---
# <a name="idebugprocess3continue"></a>IDebugProcess3::Continue
继续从已停止状态运行此过程。 保留任何以前的执行状态（如步骤），进程将再次开始执行。

> [!NOTE]
> 此方法应使用而不是["继续](../../../extensibility/debugger/reference/idebugprogram2-continue.md)"。

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
[在]表示要继续的线程的[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 无论正在调试的进程数或哪个进程生成了停止事件，此过程都会调用此方法。 实现必须保留以前的执行状态（如步骤），并继续执行，就好像在完成之前执行之前从未停止过一样。 也就是说，如果此过程中的线程执行过单操作，并且由于其他进程停止而停止，然后`Continue`被调用，则指定的线程必须完成原始跨行操作。

 **警告**在处理此调用时，不要向[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)发送停止事件或立即（同步）事件;否则调试器可能会挂起。

## <a name="see-also"></a>请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
