---
title: EVENTATTRIBUTES |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EVENTATTRIBUTES
helpviewer_keywords:
- EVENTATTRIBUTES enumeration
ms.assetid: 04db10f7-df31-4464-98e8-b3777428179e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c479058a5e6abb61fb419425706d2a8b26858d04
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737057"
---
# <a name="eventattributes"></a>EVENTATTRIBUTES
指定事件属性。

## <a name="syntax"></a>语法

```cpp
enum enum_EVENTATTRIBUTES {
    EVENT_ASYNCHRONOUS          = 0x0000,
    EVENT_SYNCHRONOUS           = 0x0001,
    EVENT_STOPPING              = 0x0002,
    EVENT_ASYNC_STOP            = 0x0002,
    EVENT_SYNC_STOP             = 0x0003,
    EVENT_IMMEDIATE             = 0x0004,
    EVENT_EXPRESSION_EVALUATION = 0x0008
};
typedef DWORD EVENTATTRIBUTES;
```

```csharp
public enum enum_EVENTATTRIBUTES {
    EVENT_ASYNCHRONOUS          = 0x0000,
    EVENT_SYNCHRONOUS           = 0x0001,
    EVENT_STOPPING              = 0x0002,
    EVENT_ASYNC_STOP            = 0x0002,
    EVENT_SYNC_STOP             = 0x0003,
    EVENT_IMMEDIATE             = 0x0004,
    EVENT_EXPRESSION_EVALUATION = 0x0008
};
```

## <a name="fields"></a>字段
`EVENT_ASYNCHRONOUS`\
指示事件是异步的，并且不需要对事件的任何回复。

`EVENT_SYNCHRONOUS`\
指示事件是同步的;通过 [ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)回复。

`EVENT_STOPPING`\
指示这是一个停止事件。 必须与或组合在 `EVENT_ASYNCHRONOUS` 一起 `EVENT_SYNCHRONOUS` 。

`EVENT_ASYNC_STOP`\
指示异步停止事件。 目前没有此类事件。 此标志只是一个占位符。

`EVENT_SYNC_STOP`\
指示同步停止事件 (和) 的组合 `EVENT_SYNCHRONOUS` `EVENT_STOPPING` 。 此值由调试引擎在发送停止事件时 (DE) 使用。 通过调用 [Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md)、 [Step](../../../extensibility/debugger/reference/idebugprogram2-step.md)或 [Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md)发出回复。

`EVENT_IMMEDIATE`\
指示将立即同步发送到 IDE 的事件。 此标志与其他标志（如、或）组合在一起， `EVENT_ASYNCHRONOUS` `EVENT_SYNCHRONOUS` `EVENT_SYNC_STOP` 以指示事件的类型，以及在已知任何) 的情况下， (回复机制。

`EVENT_EXPRESSION_EVALUATION`\
事件是表达式计算的结果。

## <a name="remarks"></a>备注
这些值在 `dwAttrib` [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) 方法的参数中传递。

这些值可以与按位组合 `OR` 。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
