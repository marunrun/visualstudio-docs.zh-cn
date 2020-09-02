---
title: IDebugAddress2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress2
helpviewer_keywords:
- IDebugAddress2 interface
ms.assetid: b150e0ed-4ac0-4f8c-9732-4b3e54b9d243
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 402d8c8bcb50c570ff680b8fe1cf8d26f037ba17
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80736566"
---
# <a name="idebugaddress2"></a>IDebugAddress2
此接口提供对拥有其地址由此接口表示的对象的进程 ID 的访问。

## <a name="syntax"></a>语法

```
IDebugAddress2 : IDebugAddress
```

## <a name="notes-for-implementers"></a>实施者注意事项
 符号提供程序在实现 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 接口的同一对象上实现此接口。 此接口提供对拥有与此地址相关的对象的进程的 ID 的访问。

## <a name="notes-for-callers"></a>调用方说明
 使用 [QueryInterface](/cpp/atl/queryinterface) 从 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 接口获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法
 除了继承自 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 接口的方法之外，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetProcessID](../../../extensibility/debugger/reference/idebugaddress2-getprocessid.md)|检索拥有此接口所表示的对象的进程的 ID。|

## <a name="requirements"></a>要求
 标头： sh。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
