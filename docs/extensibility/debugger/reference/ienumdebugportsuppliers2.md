---
title: IEnumDebugPort供应商2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPortSuppliers2
helpviewer_keywords:
- IEnumDebugPortSuppliers2
ms.assetid: cd0a73dc-dd25-46fd-8c4f-5b011501afeb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: de0bfc5b387df9b347e4a58d97601a5e1e70f1a4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715933"
---
# <a name="ienumdebugportsuppliers2"></a>IEnumDebugPortSuppliers2
此接口枚举端口供应商。

## <a name="syntax"></a>语法

```
IEnumDebugPortSuppliers2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 Visual Studio 实现此接口以表示端口供应商的列表。

## <a name="notes-for-callers"></a>呼叫者备注
 致电[EnumPort 供应商](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)以获取港口供应商列表。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IEnumDebugPortSuppliers2`。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-next.md)|在枚举序列中检索指定数量的端口供应商。|
|[跳](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-skip.md)|在枚举序列中跳过指定数量的端口供应商。|
|[重置](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-clone.md)|创建与当前枚举器相同的枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-getcount.md)|获取枚举器中的端口供应商数。|

## <a name="remarks"></a>备注
 调试引擎通常不需要获取此接口。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)
