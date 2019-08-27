---
title: IEnumDebugAddresses | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses
helpviewer_keywords:
- IEnumDebugAddresses interface
ms.assetid: 5f6f6751-e6d8-4c5a-8e81-414b6e5d8cc5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0f7871a223695632b5c2118377c9cfeb24d297e4
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329912"
---
# <a name="ienumdebugaddresses"></a>IEnumDebugAddresses
此接口表示的对象实现的集合[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)接口。

## <a name="syntax"></a>语法

```
IEnumDebugAdresses : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 此接口由符号提供程序来实现的对象集的实现[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)接口。 请注意，这不是由于存在一个标准 COM 枚举[GetCount](../../../extensibility/debugger/reference/ienumdebugaddresses-getcount.md)方法。

## <a name="notes-for-callers"></a>调用方的说明
 此接口将返回由[GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)并[GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 此接口实现以下方法。

|方法|描述|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugaddresses-next.md)|检索下一套[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)枚举中的对象。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugaddresses-skip.md)|将跳过指定的数目的条目。|
|[Reset](../../../extensibility/debugger/reference/ienumdebugaddresses-reset.md)|将枚举重置为第一个条目。|
|[Clone](../../../extensibility/debugger/reference/ienumdebugaddresses-clone.md)|检索当前枚举的副本。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugaddresses-getcount.md)|检索枚举中的条目数。|

## <a name="remarks"></a>备注
 调试引擎通常使用此接口来帮助确定相应的地址，以便向表达式计算器。

## <a name="requirements"></a>要求
 标头： sh.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)
- [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)