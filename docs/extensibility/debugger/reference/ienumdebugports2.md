---
title: IEnumDebugPorts2 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80716100"
---
# <a name="ienumdebugports2"></a>IEnumDebugPorts2
此接口枚举计算机或端口供应商的端口。

## <a name="syntax"></a>语法

```
IEnumDebugPorts2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 自定义端口供应商实现此接口，以表示供应商创建的端口列表。 Visual Studio 实现此接口以支持其自己的端口供应商。

## <a name="notes-for-callers"></a>调用方说明
 调用 [EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md) 以获取此接口，该接口表示由端口供应商创建的端口列表。 调用 [EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md) 以获取此接口，该接口表示已保存到磁盘的端口列表。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IEnumDebugPorts2` 。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugports2-next.md)|检索枚举序列中指定数量的端口。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugports2-skip.md)|跳过枚举序列中指定数量的端口。|
|[重置](../../../extensibility/debugger/reference/ienumdebugports2-reset.md)|将枚举序列重置到开始处。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugports2-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugports2-getcount.md)|获取枚举器中的端口数。|

## <a name="remarks"></a>备注
 Visual Studio 使用此接口来帮助填充用于附加到进程的端口列表。

 调试引擎通常不使用此接口。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)
- [EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)
