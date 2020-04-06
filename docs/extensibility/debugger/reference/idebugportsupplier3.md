---
title: IDebugPort供应商3 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3
helpviewer_keywords:
- IDebugPortSupplier3 interface
ms.assetid: e458cd02-2370-4435-8953-17d7a60ce152
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f015c21f71f064f2302660ebc75ef00a245348c3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724439"
---
# <a name="idebugportsupplier3"></a>IDebugPortSupplier3
此接口允许调用方确定端口供应商是否可以在调试器的调用之间保留端口（通过将它们写入磁盘），然后获取这些保留的端口的列表。

## <a name="syntax"></a>语法

```
IDebugPortSupplier3 : IDebugPortSupplier2
```

## <a name="notes-for-implementers"></a>实施者说明
 自定义端口供应商实现此接口以支持保留或将端口信息保存到磁盘。 此接口必须在与[IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)接口相同的对象上实现。

## <a name="notes-for-callers"></a>呼叫者备注
 在`IDebugPortSupplier2`接口上调用[查询接口](/cpp/atl/queryinterface)以获取此接口。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法
 除了从[IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)接口继承的方法外，此接口还支持以下功能：

|方法|描述|
|------------|-----------------|
|[CanPersistPorts](../../../extensibility/debugger/reference/idebugportsupplier3-canpersistports.md)|返回端口供应商是否可以在调试器的调用之间保留端口（通过将它们写入磁盘）。|
|[EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md)|返回可用于枚举此端口供应商写入磁盘的所有端口的对象。|

## <a name="remarks"></a>备注
 如果端口供应商可以跨调用保留端口，则应实现此接口。 当端口供应商实例化时，应加载端口，并在端口供应商销毁时写入磁盘。

 调试引擎通常不与端口供应商交互，并且对此接口没有用处。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
