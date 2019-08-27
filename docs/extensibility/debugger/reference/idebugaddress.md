---
title: IDebugAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress
helpviewer_keywords:
- IDebugAddress interface
ms.assetid: bc709ff7-4966-4f36-9af2-690efe2cea1d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 653d2424d21a18e7053f66e0a74214ecc25d97da
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66317924"
---
# <a name="idebugaddress"></a>IDebugAddress
此接口表示的项的地址。 它会返回符号处理程序。

## <a name="syntax"></a>语法

```
IDebugAddress : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 符号提供程序实现此接口来表示对象的地址。

## <a name="notes-for-callers"></a>调用方的说明
 在多个接口上的很多方法返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)|检索[DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)结构描述一个对象和其位置。|

## <a name="remarks"></a>备注
 符号提供程序返回此接口来表示对象并将其位置 （例如，函数、 方法或类） 在特定范围内。 此接口是从返回并传递给各种方法的符号提供程序和表达式计算器。 通常情况下，符号提供程序是需要解释此接口的内容的唯一实体。

## <a name="requirements"></a>要求
 标头： sh.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)