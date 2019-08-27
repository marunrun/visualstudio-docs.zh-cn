---
title: IDebugPropertyDestroyEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPropertyDestroyEvent2
helpviewer_keywords:
- IDebugPropertyDestroyEvent2 interface
ms.assetid: 301b7a75-ecfa-46f1-9131-66cf3e4be147
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a52e9a1a3723566dd7a2dbdfc3cfe1a4d41261ed
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322748"
---
# <a name="idebugpropertydestroyevent2"></a>IDebugPropertyDestroyEvent2
与特定文档相关联的属性即将被销毁时，此接口是由调试引擎 (DE) 发送到会话调试管理器 (SDM) 中。

## <a name="syntax"></a>语法

```
IDebugPropertyDestroyEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 DE 实现此接口以报告属性已被销毁。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须实现此接口作为对同一个对象。 使用 SDM [QueryInterface](/cpp/atl/queryinterface)访问`IDebugEvent2`接口。 此接口实现，如果 DE 以前创建了与脚本; 关联的属性销毁该属性从 IDE 中删除关联的脚本。

## <a name="notes-for-callers"></a>调用方的说明
 DE 创建，并将此事件对象发送到报表的属性已被销毁。 通过使用发送该事件[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) SDM 附加到正在调试的程序时提供的回调函数。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugPropertyDestroyEvent2`。

|方法|描述|
|------------|-----------------|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertydestroyevent2-getdebugproperty.md)|获取要销毁的属性。|

## <a name="remarks"></a>备注
 请参阅备注[IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md)这些事件用于有关原因的详细信息。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md)