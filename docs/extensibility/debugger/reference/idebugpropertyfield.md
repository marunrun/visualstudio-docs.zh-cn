---
title: IDebug属性字段 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPropertyField
helpviewer_keywords:
- IDebugPropertyField interface
ms.assetid: b50edb2c-fb8d-4def-993d-17d23d2027c1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 96a3f3c2dca16cd2c28c9d1727e4ac145c91c482
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720693"
---
# <a name="idebugpropertyfield"></a>IDebugPropertyField
此接口提供允许获取和设置属性的功能。

## <a name="syntax"></a>语法

```
IDebugPropertyField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>实施者说明
 符号提供程序在实现[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)的同一对象上实现此接口。 此接口是支持类上属性概念的专门化。

## <a name="notes-for-callers"></a>呼叫者备注
 如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)方法返回`FIELD_KIND_PROP`，则使用[查询接口](/cpp/atl/queryinterface)从[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)和[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口上的方法外，此接口还实现了以下方法：

|方法|描述|
|------------|-----------------|
|[GetPropertyGetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md)|获取获取属性的方法。|
|[GetPropertySetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertysetter.md)|获取设置属性的方法。|

## <a name="remarks"></a>备注
 属性是托管代码概念，表示被视为变量的方法。 属性在非托管C++中不存在。

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
