---
title: IEnumDebug绑定断点2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugBoundBreakpoints2
helpviewer_keywords:
- IEnumDebugBoundBreakpoints2
ms.assetid: ea03e7e1-28d6-40b7-8097-bbb61d3b7caa
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 421d46efbef189fd6ffc86812d2bfdd28f5da5ff
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80717442"
---
# <a name="ienumdebugboundbreakpoints2"></a>IEnumDebugBoundBreakpoints2
此接口枚举与挂起断点或断点绑定事件关联的绑定断点。

## <a name="syntax"></a>语法

```
IEnumDebugBoundBreakpoints2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口作为其对断点的支持的一部分。 如果支持断点，则必须实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
 视觉工作室呼叫：

- [EnumBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointevent2-enumbreakpoints.md)以获取此接口，表示触发的所有断点的列表。

- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)以获取此接口，表示绑定的所有断点的列表。

- [EnumBoundBreakpoint](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)以获取此接口，表示绑定到该挂起断点的的所有断点的列表。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IEnumDebugBoundBreakpoints2`。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-next.md)|检索枚举序列中指定数量的绑定断点。|
|[跳](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-skip.md)|在枚举序列中跳过指定数量的绑定断点。|
|[重置](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-clone.md)|创建与当前枚举器相同的枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-getcount.md)|获取枚举器中的绑定断点数。|

## <a name="remarks"></a>备注
 Visual Studio 使用此接口表示的绑定断点来更新 IDE 中断点的显示。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)
