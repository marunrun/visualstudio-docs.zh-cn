---
title: IDebugProcess3::Step | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Step
helpviewer_keywords:
- IDebugProcess3::Step
ms.assetid: 6ad9094c-27cc-4927-8a7c-1b4d97b2e436
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dc3ffecf5a2760077c0a5da4f4508163a48ca1a4
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66313884"
---
# <a name="idebugprocess3step"></a>IDebugProcess3::Step
将导致过程步骤一个指令或语句。

> [!NOTE]
> 应使用此方法以代替[步骤](../../../extensibility/debugger/reference/idebugprogram2-step.md)。

## <a name="syntax"></a>语法

```cpp
HRESULT Step(
   IDebugThread2* pThread,
   STEPKIND       sk,
   STEPUNIT       step,
);
```

```csharp
int Step(
   IDebugThread2 pThread,
   enum_STEPKIND sk,
   enum_STEPUNIT step
);
```

## <a name="parameters"></a>参数
`pThread`\
[in][IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象，表示正在单步执行的线程。

`sk`\
[in]之一[STEPKIND](../../../extensibility/debugger/reference/stepkind.md)值。

`step`\
[in]之一[STEPUNIT](../../../extensibility/debugger/reference/stepunit.md)值。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则将返回错误代码。

## <a name="remarks"></a>备注
 如果没有任何线程同步或线程之间的通信，当特定线程单步执行时应运行过程中的其他线程。

 **警告**stopping 事件或将即时 （同步） 事件与不发送[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)时处理此调用; 否则调试器可能会挂起。

## <a name="see-also"></a>请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [STEPKIND](../../../extensibility/debugger/reference/stepkind.md)
- [STEPUNIT](../../../extensibility/debugger/reference/stepunit.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)