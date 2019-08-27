---
title: IDebugProcess3::Continue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Continue
helpviewer_keywords:
- IDebugProcess3::Continue
ms.assetid: 57506242-5763-4c08-adb9-8a78ce02cebb
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a7d20a375644cbbac975f62db216377f271a2675
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66314047"
---
# <a name="idebugprocess3continue"></a>IDebugProcess3::Continue
将继续运行此过程从已停止状态。 保留任何以前的执行状态 （如步骤），并再次执行该过程开始。

> [!NOTE]
> 应使用此方法以代替[继续](../../../extensibility/debugger/reference/idebugprogram2-continue.md)。

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
[in][IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象，表示要继续执行的线程。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为将返回错误代码。

## <a name="remarks"></a>备注
 在此过程，不论是多少进程正在调试，或哪个进程生成 stopping 事件上调用此方法。 实现必须保留以前的执行状态 （如步骤），并继续执行，就好像它永远不会有停止之前完成其前面的执行。 也就是说，如果中的线程则此过程将已执行步骤的操作和已停止，因为其他进程已停止，然后`Continue`调用，则指定线程必须完成原始逐过程操作。

 **警告**stopping 事件或将即时 （同步） 事件与不发送[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)时处理此调用; 否则调试器可能会挂起。

## <a name="see-also"></a>请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)