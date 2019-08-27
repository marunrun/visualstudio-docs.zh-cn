---
title: IEnumDebugPortSuppliers2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPortSuppliers2
helpviewer_keywords:
- IEnumDebugPortSuppliers2
ms.assetid: cd0a73dc-dd25-46fd-8c4f-5b011501afeb
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 39d9d9462fe1951f01927b9180fa8a99aee535be
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66326396"
---
# <a name="ienumdebugportsuppliers2"></a>IEnumDebugPortSuppliers2
此接口枚举端口提供程序。

## <a name="syntax"></a>语法

```
IEnumDebugPortSuppliers2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 Visual Studio 实现此接口来表示端口供应商提供的列表。

## <a name="notes-for-callers"></a>调用方的说明
 调用[EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)来获取端口供应商提供的列表。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IEnumDebugPortSuppliers2`。

|方法|描述|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-next.md)|检索指定的数目的枚举序列中的端口提供程序。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-skip.md)|跳过枚举序列中的端口供应商提供的指定的数目。|
|[Reset](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-reset.md)|将枚举序列重置到开头。|
|[Clone](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-getcount.md)|获取一个枚举器中的端口供应商提供的数量。|

## <a name="remarks"></a>备注
 调试引擎通常不会不需要获取此接口。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)