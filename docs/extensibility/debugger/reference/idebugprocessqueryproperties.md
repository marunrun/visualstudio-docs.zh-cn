---
title: IDebugProcessQueryProperties | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessQueryProperties
ms.assetid: ce29a248-81a0-42c0-99a7-1606e8c548ec
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2ddb98c2d7e63fc27ad1469dfbfc76eaaee38582
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353105"
---
# <a name="idebugprocessqueryproperties"></a>IDebugProcessQueryProperties
此接口是实现的扩展接口[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)实施者。 它允许实施者可以获取有关调试的进程环境的信息。

## <a name="syntax"></a>语法

```
IDebugProcessQueryProperties: IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 实现此接口，以获取有关调试的进程的执行环境信息。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugProcessQueryProperties`。

|方法|描述|
|------------|-----------------|
|[QueryProperty](../../../extensibility/debugger/reference/idebugprocessqueryproperties-queryproperty.md)|属性值的查询。|
|[QueryProperties](../../../extensibility/debugger/reference/idebugprocessqueryproperties-queryproperties.md)|查询的属性值。|

## <a name="remarks"></a>备注
 很少实现此接口。

## <a name="requirements"></a>要求
 标头：Portpriv.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)