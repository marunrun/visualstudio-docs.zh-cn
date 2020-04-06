---
title: IDebugPortNotify2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortNotify2
helpviewer_keywords:
- IDebugPortNotify2 interface
ms.assetid: 43278b79-bf16-4c08-bcf1-6f7f7a17feab
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 49d3d1161d488ed4a9e12b7af6b70bf336c9f286
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724917"
---
# <a name="idebugportnotify2"></a>IDebugPortNotify2
此接口注册或取消注册一个程序，该程序可以使用正在运行的端口进行调试。

## <a name="syntax"></a>语法

```
IDebugPortNotify2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 自定义端口供应商实现此接口以支持从端口添加和删除程序。 它通常实现在实现[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)接口的同一对象上。

## <a name="notes-for-callers"></a>呼叫者备注
 对接口上的[查询接口](/cpp/atl/queryinterface)的`IDebugPort2`调用将返回此接口。 此外，对[GetPortNotify 的](../../../extensibility/debugger/reference/idebugdefaultport2-getportnotify.md)调用将返回此接口。 调试引擎可以将此接口视为[WatchForProvider 事件的](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)参数。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugPortNotify2`。

|方法|描述|
|------------|-----------------|
|[AddProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)|注册一个程序，该程序可以使用正在运行的端口进行调试。|
|[RemoveProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)|取消注册可以从正在运行的端口调试的程序。|

## <a name="remarks"></a>备注
 除非调试端口有一种方法来知道何时加载或卸载程序，否则自定义端口供应商必须实现此接口。 使用此接口跟踪加载用于通过特定端口进行调试的所有程序。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
