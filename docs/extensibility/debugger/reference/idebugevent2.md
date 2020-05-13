---
title: IDebugEvent2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEvent2
helpviewer_keywords:
- IDebugEvent2 interface
ms.assetid: de3d714d-96fb-4e12-b66b-a75391472153
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a6341f8003b962a7f45420b076b23623ebdaf861
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729908"
---
# <a name="idebugevent2"></a>IDebugEvent2
此接口用于通信关键调试信息（如断点停止）和非关键信息（如调试消息）。

## <a name="syntax"></a>语法

```
IDebugEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 和自定义端口供应商在与所有其他事件接口相同的对象上实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
 使用提供给[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)或[事件的](../../../extensibility/debugger/reference/idebugportevents2-event.md)接口 ID （IID） 参数，会话调试管理器 （SDM） 调用`IDebugEvent2`接口上的[QueryInterface](/cpp/atl/queryinterface)以获取适当的事件接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugEvent2`。

|方法|描述|
|------------|-----------------|
|[获取属性](../../../extensibility/debugger/reference/idebugevent2-getattributes.md)|获取此调试事件的属性。|

## <a name="remarks"></a>备注
 更具体的事件接口（如[IDebugBreakpointEvent2）](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)不派生自 IDebugEvent2 接口，而是作为与`IDebugEvent2`的相同对象上的单独接口实现。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
