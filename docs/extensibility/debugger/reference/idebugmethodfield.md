---
title: IDebugMethodfield |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField
helpviewer_keywords:
- IDebugMethodField interface
ms.assetid: a7dc9030-fc98-4cf1-b943-37a4003300b6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 061035933e57ea4ca8e7857f68ac3d6311bae32c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727062"
---
# <a name="idebugmethodfield"></a>IDebugMethodField
此接口描述方法。

## <a name="syntax"></a>语法

```
IDebugMethodField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>实施者说明
 符号提供程序在实现[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口的同一对象上实现此接口。 此接口是一个专门化，它提供了一个方法。

## <a name="notes-for-callers"></a>呼叫者备注
 如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)返回`FIELD_TYPE_METHOD`，请使用[查询接口](/cpp/atl/queryinterface)从[IDebug 容器字段](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口获取此接口。 此外，方法[，GetPropertyGetter，GetPropertySetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md)和[枚举构建器](../../../extensibility/debugger/reference/idebugclassfield-enumconstructors.md)，都返回接口`IDebugMethodField`。 [GetPropertySetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertysetter.md)

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)和[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口上的方法外，此接口还实现了以下方法：

|方法|描述|
|------------|-----------------|
|[EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md)|为方法的参数创建枚举器。|
|[GetThis](../../../extensibility/debugger/reference/idebugmethodfield-getthis.md)|获取包含方法的对象的"this"指针。|
|[EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)|为方法的所有局部变量创建枚举器。|
|[EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)|为方法的选定局部变量创建枚举器。|
|[IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugmethodfield-iscustomattributedefined.md)|确定是否已定义特定的自定义属性。|
|[EnumStaticLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumstaticlocals.md)|为方法的静态局部变量创建枚举器。|
|[GetGlobalContainer](../../../extensibility/debugger/reference/idebugmethodfield-getglobalcontainer.md)|获取 方法的全局容器。|
|[EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)|为调用方法所需的每个参数的类型创建枚举器。|

## <a name="remarks"></a>备注
 方法可以包含参数和局部变量。

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
