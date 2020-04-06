---
title: IDebug自定义属性查询2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2
helpviewer_keywords:
- IDebugCustomAttributeQuery interface
- IDebugCustomAttributeQuery2 interface
ms.assetid: 7cfa23e4-a05a-47a3-af6c-bd40c655014b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6fe3969002c64ab361de76012c432e2bb5c61b5c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732486"
---
# <a name="idebugcustomattributequery2"></a>IDebugCustomAttributeQuery2
确定此字段的自定义属性的存在，如果存在，则返回属性信息。

## <a name="syntax"></a>语法

```
IDebugCustomAttributeQuery2 : IDebugCustomAttributeQuery
```

## <a name="notes-for-implementers"></a>实施者说明
 符号提供程序在实现[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)的同一对象上实现此接口，以支持自定义属性。

## <a name="notes-for-callers"></a>呼叫者备注
 使用[查询接口](/cpp/atl/queryinterface)从[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了**IDebugCustom属性查询**接口的方法。

|方法|描述|
|------------|-----------------|
|[IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)|确定自定义属性是否存在名称。|
|[GetCustomAttributeByName](../../../extensibility/debugger/reference/idebugcustomattributequery2-getcustomattributebyname.md)|获取给定自定义属性的属性信息。|

 除了**IDebugCustom属性查询**方法之外，`IDebugCustomAttributeQuery2`实现以下方法：

|方法|描述|
|------------|-----------------|
|[EnumCustomAttributes](../../../extensibility/debugger/reference/idebugcustomattributequery2-enumcustomattributes.md)|获取附加到此字段的所有自定义属性的枚举器。|

## <a name="remarks"></a>备注
 [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)方法可以为此字段定义的所有自定义属性返回枚举器。

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
