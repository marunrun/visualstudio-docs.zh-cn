---
title: IDebugarrayfield |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayField
helpviewer_keywords:
- IDebugArrayField interface
ms.assetid: 9667b0a5-4295-46cc-9388-b75c1350be15
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dab01c1e956ced7e6894b951ab16f4ce68eb778b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736289"
---
# <a name="idebugarrayfield"></a>IDebugArrayField
此接口描述数组符号或类型。

## <a name="syntax"></a>语法

```
IDebugArrayField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>实施者说明
 符号提供程序在实现[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口的同一对象上实现此接口。 此接口是表示数组对象的专门化。

## <a name="notes-for-callers"></a>呼叫者备注
 如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)返回标志`FIELD_TYPE_ARRAY`，则使用[查询接口](/cpp/atl/queryinterface)从[IDebug 容器字段](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)和[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口上的方法外，此接口还实现了以下功能：

|方法|描述|
|------------|-----------------|
|[GetNumberOfElements](../../../extensibility/debugger/reference/idebugarrayfield-getnumberofelements.md)|获取数组中的元素数。|
|[GetElementType](../../../extensibility/debugger/reference/idebugarrayfield-getelementtype.md)|获取数组中的元素类型。|
|[GetRank](../../../extensibility/debugger/reference/idebugarrayfield-getrank.md)|获取数组的排名。|

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
