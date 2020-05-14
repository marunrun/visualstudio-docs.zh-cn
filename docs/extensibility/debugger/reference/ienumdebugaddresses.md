---
title: IEnum调试地址 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses
helpviewer_keywords:
- IEnumDebugAddresses interface
ms.assetid: 5f6f6751-e6d8-4c5a-8e81-414b6e5d8cc5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 14b42ec37babe72b47b0e832397d33029c4fc3d1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80717586"
---
# <a name="ienumdebugaddresses"></a>IEnumDebugAddresses
此接口表示实现[IDebugAddress 接口](../../../extensibility/debugger/reference/idebugaddress.md)的对象的集合。

## <a name="syntax"></a>语法

```
IEnumDebugAdresses : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 此接口由符号提供程序实现，以提供实现[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)接口的对象集。 请注意，由于[存在 GetCount](../../../extensibility/debugger/reference/ienumdebugaddresses-getcount.md)方法，这不是标准 COM 枚举。

## <a name="notes-for-callers"></a>呼叫者备注
 此接口由[从上下文获取地址](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)和[从位置获取地址](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)返回。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法
 此接口实现以下方法。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumdebugaddresses-next.md)|从枚举中检索下一组[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)对象。|
|[跳](../../../extensibility/debugger/reference/ienumdebugaddresses-skip.md)|跳过指定数量的条目。|
|[重置](../../../extensibility/debugger/reference/ienumdebugaddresses-reset.md)|将枚举重置为第一个条目。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugaddresses-clone.md)|检索当前枚举的副本。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugaddresses-getcount.md)|检索枚举中的条目数。|

## <a name="remarks"></a>备注
 调试引擎通常使用此接口来帮助确定要向表达式赋值器提供的适当地址。

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)
- [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)
