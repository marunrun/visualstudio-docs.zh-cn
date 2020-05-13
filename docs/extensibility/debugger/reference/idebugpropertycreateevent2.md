---
title: IDebug属性创建事件2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPropertyCreateEvent2
helpviewer_keywords:
- IDebugPropertyCreateEvent2 interface
ms.assetid: 33b3082b-a42e-488a-a1e4-dadf506f922c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 84d8fcb4375f29820b51752ac3fdebbd04f06f80
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720931"
---
# <a name="idebugpropertycreateevent2"></a>IDebugPropertyCreateEvent2
此接口由调试引擎 （DE） 发送到会话调试管理器 （SDM） 时，它创建与特定文档关联的属性。

## <a name="syntax"></a>语法

```
IDebugPropertyCreateEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 DE 实现此接口以报告已创建属性。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现。 SDM 使用[查询接口](/cpp/atl/queryinterface)访问`IDebugEvent2`接口。 如果 DE 创建了与已加载或创建的脚本关联的属性，并且该脚本需要显示在 IDE 中，则实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
 DE 创建并发送此事件对象以报告已创建属性。 该事件使用 SDM 在附加到正在调试的程序时提供的[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)回调函数进行发送。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了`IDebugPropertyCreateEvent2`接口的方法。

|方法|描述|
|------------|-----------------|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertycreateevent2-getdebugproperty.md)|获取新属性。|

## <a name="remarks"></a>备注
 如果属性具有与其关联的特定文档或脚本，DE 可以将此事件发送到 SDM，以便使用文档的名称更新**脚本文档**窗口。 SDM 将使用 参数`guidDocument`调用[GetExtendedInfo](../../../extensibility/debugger/reference/idebugproperty2-getextendedinfo.md)以`VARIANT`检索包含[I 未知指针的](/cpp/atl/iunknown)指针。 SDM 将在此指针上调用[QueryInterface](/cpp/atl/queryinterface)以检索用于更新**脚本文档**窗口的[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)接口。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
