---
title: IEnumDebugPorts2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPorts2
helpviewer_keywords:
- IEnumDebugPorts2
ms.assetid: 1754eef3-cf62-42e0-b218-1911acba77d4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c24edcd5ef47408cd4c11b3d0548ad34516702a1
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66326507"
---
# <a name="ienumdebugports2"></a>IEnumDebugPorts2
此接口枚举的计算机或端口供应商提供的端口。

## <a name="syntax"></a>语法

```
IEnumDebugPorts2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 自定义端口提供程序实现此接口来表示一系列由供应商创建的端口。 Visual Studio 实现此接口来支持其自己的端口提供程序。

## <a name="notes-for-callers"></a>调用方的说明
 调用[EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)若要获取此界面表示创建的端口提供程序的端口的列表。 调用[EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md)获取表示已保存的端口的列表的此接口到磁盘。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IEnumDebugPorts2`。

|方法|描述|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugports2-next.md)|检索指定的数目的枚举序列中的端口。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugports2-skip.md)|将跳过指定的数目的枚举序列中的端口。|
|[Reset](../../../extensibility/debugger/reference/ienumdebugports2-reset.md)|将枚举序列重置到开头。|
|[Clone](../../../extensibility/debugger/reference/ienumdebugports2-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugports2-getcount.md)|获取一个枚举器中的端口数。|

## <a name="remarks"></a>备注
 Visual Studio 将此接口来填充附加到进程所用端口的列表。

 通常，调试引擎不使用此接口。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)
- [EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)