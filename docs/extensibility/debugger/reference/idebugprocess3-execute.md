---
title: IDebugProcess3::Execute | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Execute
helpviewer_keywords:
- IDebugProcess3::Execute
ms.assetid: d831cd81-d7bf-4172-8517-aa699867791f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6b4b854c752bc7b1f66687074fbfe86286fc48fb
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66314006"
---
# <a name="idebugprocess3execute"></a>IDebugProcess3::Execute
将继续运行此过程从已停止状态。 清除任何以前的执行状态 （如步骤），并再次执行该过程开始。

> [!NOTE]
> 应使用此方法以代替[Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md)。

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
[in][IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象，表示要执行的线程。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为将返回错误代码。

## <a name="remarks"></a>备注
 当用户从某个其他进程的线程已停止状态开始执行时，对此过程将调用此方法。 当用户选择此方法也称为**启动**命令**调试**菜单在 IDE 中的。 此方法的实现可能很简单，与调用[Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md)过程中在当前线程上的方法。

> [!WARNING]
> 不发送停止事件或将即时 （同步） 事件与[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)时处理此调用; 否则调试器可能会挂起。

## <a name="see-also"></a>请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)