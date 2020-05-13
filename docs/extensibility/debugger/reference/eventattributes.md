---
title: 事件属性 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
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
指示事件是异步的，不需要对该事件进行回复。

`EVENT_SYNCHRONOUS`\
指示事件是同步的;通过["继续从同步事件](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)"进行回复。

`EVENT_STOPPING`\
指示这是停止事件。 必须与 或`EVENT_ASYNCHRONOUS``EVENT_SYNCHRONOUS`合并。

`EVENT_ASYNC_STOP`\
指示异步停止事件。 目前没有此类事件。 此标志仅是占位符。

`EVENT_SYNC_STOP`\
指示同步停止事件（和`EVENT_SYNCHRONOUS``EVENT_STOPPING`的组合）。 当调试引擎 （DE） 发送停止事件时，将使用此值。 答复是通过调用[执行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)、[步骤](../../../extensibility/debugger/reference/idebugprogram2-step.md)或[继续](../../../extensibility/debugger/reference/idebugprogram2-continue.md)。

`EVENT_IMMEDIATE`\
指示立即同步发送到 IDE 的事件。 此标志与其他标志（如`EVENT_ASYNCHRONOUS`，）`EVENT_SYNCHRONOUS`结合`EVENT_SYNC_STOP`使用，或指示事件的类型以及已知答复机制（如果有）的事实。

`EVENT_EXPRESSION_EVALUATION`\
该事件是表达式计算的结果。

## <a name="remarks"></a>备注
这些值在[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)方法的`dwAttrib`参数中传递。

这些值可以稍微结合`OR`。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
