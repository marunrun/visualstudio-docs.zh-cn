---
title: IDebugCustomAttributeQuery2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2
helpviewer_keywords:
- IDebugCustomAttributeQuery interface
- IDebugCustomAttributeQuery2 interface
ms.assetid: 7cfa23e4-a05a-47a3-af6c-bd40c655014b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 00220574ac9c16bdab9abd64adde1877ee0fd9f2
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66335805"
---
# <a name="idebugcustomattributequery2"></a>IDebugCustomAttributeQuery2
确定存在此字段的自定义属性，并且如果存在，将返回属性信息。

## <a name="syntax"></a>语法

```
IDebugCustomAttributeQuery2 : IDebugCustomAttributeQuery
```

## <a name="notes-for-implementers"></a>实施者的说明
 符号提供程序实现此接口上实现的相同对象[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)以支持自定义属性。

## <a name="notes-for-callers"></a>调用方的说明
 使用[QueryInterface](/cpp/atl/queryinterface)若要获取此接口从[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法**IDebugCustomAttributeQuery**接口。

|方法|描述|
|------------|-----------------|
|[IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)|确定名称是否存在自定义属性。|
|[GetCustomAttributeByName](../../../extensibility/debugger/reference/idebugcustomattributequery2-getcustomattributebyname.md)|获取给定的自定义特性的属性信息。|

 除了**IDebugCustomAttributeQuery**方法，`IDebugCustomAttributeQuery2`实现以下方法：

|方法|描述|
|------------|-----------------|
|[EnumCustomAttributes](../../../extensibility/debugger/reference/idebugcustomattributequery2-enumcustomattributes.md)|获取附加到此字段的所有自定义属性的枚举器。|

## <a name="remarks"></a>备注
 [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)方法可返回为此字段定义的所有自定义属性的枚举器。

## <a name="requirements"></a>要求
 标头： sh.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)