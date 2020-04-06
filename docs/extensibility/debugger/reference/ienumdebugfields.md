---
title: IEnum调试场 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFields
helpviewer_keywords:
- IEnumDebugFields interface
ms.assetid: 403c2a51-3ba5-431f-a1dd-2f3b2046c00c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d577ff2f5848f2cb348bcaccf57875507018634b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716778"
---
# <a name="ienumdebugfields"></a>IEnumDebugFields
此接口表示实现[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口的对象的集合。

## <a name="syntax"></a>语法

```
IEnumDebugFields : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 此接口由符号提供程序实现，以提供实现[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口的对象集。 请注意，由于[存在 GetCount](../../../extensibility/debugger/reference/ienumdebugfields-getcount.md)方法，这不是标准 COM 枚举。

## <a name="notes-for-callers"></a>呼叫者备注
 此接口由[GetMethodFieldsBy名称](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md)和[获取名称空间已使用At地址](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)返回。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法
 此接口实现以下方法。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumdebugfields-next.md)|从枚举中检索下一组[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象。|
|[跳](../../../extensibility/debugger/reference/ienumdebugfields-skip.md)|跳过指定数量的条目。|
|[重置](../../../extensibility/debugger/reference/ienumdebugfields-reset.md)|将枚举重置为第一个条目。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugfields-clone.md)|检索当前枚举的副本。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugfields-getcount.md)|检索枚举中的条目数。|

## <a name="remarks"></a>备注

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md)
- [GetNamespacesUsedAtAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)
