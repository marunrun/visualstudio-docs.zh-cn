---
title: IDebug 突破点事件2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointEvent2
helpviewer_keywords:
- IDebugBreakpointEvent2 interface
ms.assetid: 50b3a7a7-331b-42c8-922c-ff3522ebe1da
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f59bdef49f5c7b9c4dc345ba1862f3f08042428e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735026"
---
# <a name="idebugbreakpointevent2"></a>IDebugBreakpointEvent2
当程序停止在断点时，调试引擎 （DE） 会将此接口发送到会话调试管理器 （SDM）。

## <a name="syntax"></a>语法

```
IDebugBreakpointEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 DE 实现此接口作为其对断点的支持的一部分。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现（SDM 使用[查询接口](/cpp/atl/queryinterface)访问`IDebugEvent2`接口）。

## <a name="notes-for-callers"></a>呼叫者备注
 当程序中遇到至少一个断点时，DE 将创建并发送此事件对象。 该事件使用 SDM 提供的[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)回调功能在附加到正在调试的程序时发送。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugBreakpointEvent2`。

|方法|描述|
|------------|-----------------|
|[EnumBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointevent2-enumbreakpoints.md)|为在当前代码位置触发的所有断点创建枚举器。|

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
