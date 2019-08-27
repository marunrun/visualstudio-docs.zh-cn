---
title: IDebugPortSupplierLocale2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierLocale2 interface
ms.assetid: 910e7220-da2a-4339-9fff-9fb1bad3c28c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1f691bba978243e75511996caee38df09baa3c3e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353299"
---
# <a name="idebugportsupplierlocale2"></a>IDebugPortSupplierLocale2
为端口供应商提供的区域设置支持。

## <a name="syntax"></a>语法

```
IDebugPortSupplierLocale2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 自定义端口提供程序实现此接口可设置的区域设置。

## <a name="methods"></a>方法
 下表显示的方法**IDebugPortSupplierLocale2**。

|方法|描述|
|------------|-----------------|
|[SetLocale](../../../extensibility/debugger/reference/idebugportsupplierlocale2-setlocale.md)|为端口提供程序设置的区域设置。|

## <a name="requirements"></a>要求
 标头：Portpriv.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)