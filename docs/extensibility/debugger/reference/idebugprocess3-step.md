---
title: IDebugProcess3：：步骤 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Step
helpviewer_keywords:
- IDebugProcess3::Step
ms.assetid: 6ad9094c-27cc-4927-8a7c-1b4d97b2e436
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c5c4927f3f997b7fdbdca2b32977f2aa31a51219
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723548"
---
# <a name="idebugprocess3step"></a>IDebugProcess3::Step
使进程步长为一个指令或语句。

> [!NOTE]
> 此方法应改为[步骤](../../../extensibility/debugger/reference/idebugprogram2-step.md)。

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
[在][IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象，表示要踩的线程。

`sk`\
[在][STEPKIND](../../../extensibility/debugger/reference/stepkind.md)值之一。

`step`\
[在][STEPUNIT](../../../extensibility/debugger/reference/stepunit.md)值之一。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则返回错误代码。

## <a name="remarks"></a>备注
 如果线程之间存在任何线程同步或通信，则当特定线程正在单步执行时，进程中的其他线程应运行。

 **警告**在处理此调用时，不要向[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)发送停止事件或立即（同步）事件;否则调试器可能会挂起。

## <a name="see-also"></a>请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [STEPKIND](../../../extensibility/debugger/reference/stepkind.md)
- [STEPUNIT](../../../extensibility/debugger/reference/stepunit.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
