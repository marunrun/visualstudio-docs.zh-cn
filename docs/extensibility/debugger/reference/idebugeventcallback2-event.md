---
title: IDebugEventCallback2：： Event |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80729898"
---
# <a name="idebugeventcallback2event"></a>IDebugEventCallback2::Event
发送调试事件的通知。

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
中 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) 对象，表示发送此事件 (DE) 的调试引擎。 填写此参数需要取消。

`pProcess`\
中一个 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) 对象，该对象表示发生事件的进程。 此参数由会话调试管理器 (SDM) 填充。 DE 始终为此参数传递 null 值。

`pProgram`\
中一个 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 对象，该对象表示发生此事件的程序。 对于大多数事件，此参数不是 null 值。

`pThread`\
中一个 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) 对象，该对象表示发生此事件的线程。 对于停止事件，此参数不能为 null 值，因为从此参数获取了堆栈帧。

`pEvent`\
中表示调试事件的 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 对象。

`riidEvent`\
中标识要从参数中获取的事件接口的 GUID `pEvent` 。

`dwAttrib`\
中 [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md) 枚举中的标志的组合。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法时， `dwAttrib` 参数必须与在参数中传递的事件对象上的 [GetAttributes](../../../extensibility/debugger/reference/idebugevent2-getattributes.md) 方法所返回的值相匹配 `pEvent` 。

 所有调试事件都是异步发布的，而不管事件本身是否是异步的。 当 DE 调用此方法时，返回值不指示是否已处理事件，而只指示事件是否已收到。 事实上，在大多数情况下，此方法返回时尚未处理事件。

## <a name="see-also"></a>另请参阅
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md)
