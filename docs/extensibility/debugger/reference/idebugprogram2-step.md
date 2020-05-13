---
title: IDebugProgram2：：步骤 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Step
helpviewer_keywords:
- IDebugProgram2::Step
ms.assetid: e4c2ffce-9810-4088-8162-eac9ef04f2a9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 194e72eba5a3f137e4650752a090d91ad7c402fa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722759"
---
# <a name="idebugprogram2step"></a>IDebugProgram2::Step
执行步骤。

> [!NOTE]
> 不推荐使用此方法。 改用[步骤](../../../extensibility/debugger/reference/idebugprocess3-step.md)方法。

## <a name="syntax"></a>语法

```cpp
HRESULT Step( 
   IDebugThread2*  pThread,
   STEPKIND        sk,
   STEPUNIT        step
);
```

```csharp
int Step( 
   IDebugThread2  pThread,
   enum_STEPKIND  sk,
   enum_STEPUNIT  step
);
```

## <a name="parameters"></a>参数
`pThread`\
[在]表示正在踩走的线程的[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象。

`sk`\
[在][STEPKIND](../../../extensibility/debugger/reference/stepkind.md)枚举中指定步骤类型的值。

`step`\
[在][STEPUNIT](../../../extensibility/debugger/reference/stepunit.md)枚举中指定步进单位的值（例如，通过语句或指令）。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 如果线程之间存在任何线程同步或通信，则当特定线程正在单步执行时，程序中的其他线程应运行。

> [!WARNING]
> 在处理此调用时，不要向[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)发送停止事件或立即（同步）事件;否则调试器可能会挂起。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
