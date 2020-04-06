---
title: IDebugEvent回拨2：：事件 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEventCallback2::Event
helpviewer_keywords:
- IDebugEventCallback2::Event
ms.assetid: e5a3345b-d460-4e40-8f5b-3111c56a2ed9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0b60c09b21d531326e343dddd2f1cc69cfb0e5d2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729898"
---
# <a name="idebugeventcallback2event"></a>IDebugEventCallback2::Event
发送调试事件通知。

## <a name="syntax"></a>语法

```cpp
HRESULT Event( 
   IDebugEngine2*  pEngine,
   IDebugProcess2* pProcess,
   IDebugProgram2* pProgram,
   IDebugThread2*  pThread,
   IDebugEvent2*   pEvent,
   REFIID          riidEvent,
   DWORD           dwAttrib
);
```

```csharp
int Event( 
   IDebugEngine2  pEngine,
   IDebugProcess2 pProcess,
   IDebugProgram2 pProgram,
   IDebugThread2  pThread,
   IDebugEvent2   pEvent,
   ref Guid       riidEvent,
   uint           dwAttrib
);
```

## <a name="parameters"></a>参数
`pEngine`\
[在]表示发送此事件的调试引擎 （DE） 的[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)对象。 需要 DE 来填写此参数。

`pProcess`\
[在][IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)对象，表示事件发生的进程。 此参数由会话调试管理器 （SDM） 填充。 DE 始终传递此参数的 null 值。

`pProgram`\
[在][IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象，表示发生此事件的程序。 对于大多数事件，此参数不是 null 值。

`pThread`\
[在][IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象，表示发生此事件的线程。 对于停止事件，此参数不能为空值，因为堆栈帧是从此参数获取的。

`pEvent`\
[在]表示调试事件的[IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)对象。

`riidEvent`\
[在]GUID，用于标识要从`pEvent`参数获取的事件接口。

`dwAttrib`\
[在][事件属性](../../../extensibility/debugger/reference/eventattributes.md)枚举中标志的组合。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法时，`dwAttrib`参数必须与从[GetAttributes](../../../extensibility/debugger/reference/idebugevent2-getattributes.md)方法返回的值匹配，因为在`pEvent`参数中传递的事件对象上调用了该值。

 所有调试事件都是异步发布的，无论事件本身是否是异步的。 当 DE 调用此方法时，返回值不指示事件是否已处理，仅指示是否接收了事件。 事实上，在大多数情况下，当此方法返回时，事件尚未处理。

## <a name="see-also"></a>请参阅
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md)
