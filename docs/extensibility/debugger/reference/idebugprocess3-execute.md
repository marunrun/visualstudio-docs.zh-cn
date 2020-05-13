---
title: IDebugProcess3：：执行 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Execute
helpviewer_keywords:
- IDebugProcess3::Execute
ms.assetid: d831cd81-d7bf-4172-8517-aa699867791f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 444eadcce38adbd8ecd8655e8e0dc3f36f446848
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723683"
---
# <a name="idebugprocess3execute"></a>IDebugProcess3::Execute
继续从已停止状态运行此过程。 清除任何以前的执行状态（如步骤），进程将再次开始执行。

> [!NOTE]
> 此方法应改为[执行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)。

## <a name="syntax"></a>语法

```cpp
HRESULT Execute(
   IDebugThread2* pThread
);
```

```csharp
int Execute(
   IDebugThread2 pThread
);
```

## <a name="parameters"></a>参数
`pThread`\
[在]表示要执行的线程的[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 当用户从其他进程线程中的停止状态开始执行时，此过程将调用此方法。 当用户从 IDE 中的 **"调试"** 菜单中选择 **"开始"** 命令时，也会调用此方法。 此方法的实现可能非常简单，例如在进程中的当前线程上调用[Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md)方法。

> [!WARNING]
> 在处理此调用时，不要向[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)发送停止事件或立即（同步）事件;否则调试器可能会挂起。

## <a name="see-also"></a>请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [恢复](../../../extensibility/debugger/reference/idebugthread2-resume.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
