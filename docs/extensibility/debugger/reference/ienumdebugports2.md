---
title: IEnum调试端口2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPorts2
helpviewer_keywords:
- IEnumDebugPorts2
ms.assetid: 1754eef3-cf62-42e0-b218-1911acba77d4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f3cc46ef8abb6ef1fbb8f072d97b0fc4a537af1a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716100"
---
# <a name="ienumdebugports2"></a>IEnumDebugPorts2
此接口枚举机器或端口供应商的端口。

## <a name="syntax"></a>语法

```
IEnumDebugPorts2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 自定义端口供应商实现此接口以表示供应商创建的端口列表。 Visual Studio 实现此接口以支持其自己的端口供应商。

## <a name="notes-for-callers"></a>呼叫者备注
 调用[EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)以获取此接口，表示端口供应商创建的端口列表。 调用[EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md)以获取此接口，表示保存到磁盘的端口列表。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IEnumDebugPorts2`。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumdebugports2-next.md)|检索枚举序列中指定数量的端口。|
|[跳](../../../extensibility/debugger/reference/ienumdebugports2-skip.md)|在枚举序列中跳过指定数量的端口。|
|[重置](../../../extensibility/debugger/reference/ienumdebugports2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugports2-clone.md)|创建与当前枚举器相同的枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugports2-getcount.md)|获取枚举器中的端口数。|

## <a name="remarks"></a>备注
 Visual Studio 使用此接口帮助填充用于附加到进程的端口列表。

 调试引擎通常不使用此接口。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)
- [EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)
