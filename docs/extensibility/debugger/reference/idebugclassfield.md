---
title: IDebugClassfield |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField
helpviewer_keywords:
- IDebugClassField interface
ms.assetid: 49358cbc-8973-4862-9dcc-79b1248e6712
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 11b0e4cd7c851e65edf299f45ec97273804c25d8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734288"
---
# <a name="idebugclassfield"></a>IDebugClassField
此接口将类表示为类型。

## <a name="syntax"></a>语法

```
IDebugClassField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>实施者说明
 符号提供程序在实现[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口的同一对象上实现此接口。 此接口是表示类类型的专门化。

## <a name="notes-for-callers"></a>呼叫者备注
 许多接口都有可以返回此接口的方法，包括[IDebugSymbolProvider、IDebugMethodField](../../../extensibility/debugger/reference/idebugsymbolprovider.md)和[IDebugCustom属性](../../../extensibility/debugger/reference/idebugcustomattribute.md)。 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md) 此外，如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)方法返回标志`FIELD_TYPE_CLASS`，则可以使用[QueryInterface](/cpp/atl/queryinterface)从[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)和[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口上的方法外，此接口还实现了以下功能：

|方法|描述|
|------------|-----------------|
|[EnumBaseClasses](../../../extensibility/debugger/reference/idebugclassfield-enumbaseclasses.md)|为此类的基类创建枚举器。|
|[DoesInterfaceExist](../../../extensibility/debugger/reference/idebugclassfield-doesinterfaceexist.md)|确定是否在类中定义了特定接口。|
|[EnumNestedClasses](../../../extensibility/debugger/reference/idebugclassfield-enumnestedclasses.md)|为此类的嵌套类创建枚举器。|
|[GetEnclosingClass](../../../extensibility/debugger/reference/idebugclassfield-getenclosingclass.md)|获取包含此类的类。|
|[EnumInterfacesImplemented](../../../extensibility/debugger/reference/idebugclassfield-enuminterfacesimplemented.md)|为此类实现的接口创建枚举器。|
|[EnumConstructors](../../../extensibility/debugger/reference/idebugclassfield-enumconstructors.md)|为此类的构造函数创建枚举器。|
|[GetDefaultIndexer](../../../extensibility/debugger/reference/idebugclassfield-getdefaultindexer.md)|获取默认索引器的名称。|
|[EnumNestedEnums](../../../extensibility/debugger/reference/idebugclassfield-enumnestedenums.md)|为此类的嵌套枚举器创建枚举器。|

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
