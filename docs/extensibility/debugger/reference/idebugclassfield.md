---
title: IDebugClassField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField
helpviewer_keywords:
- IDebugClassField interface
ms.assetid: 49358cbc-8973-4862-9dcc-79b1248e6712
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 05d01ee3867481b8ab9bb100f2623c1197492666
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329453"
---
# <a name="idebugclassfield"></a>IDebugClassField
此接口作为类型表示的类。

## <a name="syntax"></a>语法

```
IDebugClassField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>实施者的说明
 符号提供程序实现此接口上实现的相同对象[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口。 此接口是表示类类型的专用化。

## <a name="notes-for-callers"></a>调用方的说明
 多个接口有方法可以返回此接口包括[IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)， [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)，并[IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)。 此外，可以使用[QueryInterface](/cpp/atl/queryinterface)若要获取此接口从[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)方法返回的标志`FIELD_TYPE_CLASS`。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了上的方法[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)并[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口，此接口实现了：

|方法|描述|
|------------|-----------------|
|[EnumBaseClasses](../../../extensibility/debugger/reference/idebugclassfield-enumbaseclasses.md)|创建此类的基类的一个枚举器。|
|[DoesInterfaceExist](../../../extensibility/debugger/reference/idebugclassfield-doesinterfaceexist.md)|确定是否在类中定义的特定接口。|
|[EnumNestedClasses](../../../extensibility/debugger/reference/idebugclassfield-enumnestedclasses.md)|创建此类的嵌套类的枚举器。|
|[GetEnclosingClass](../../../extensibility/debugger/reference/idebugclassfield-getenclosingclass.md)|获取包含此类的类。|
|[EnumInterfacesImplemented](../../../extensibility/debugger/reference/idebugclassfield-enuminterfacesimplemented.md)|创建此类实现的接口的枚举器。|
|[EnumConstructors](../../../extensibility/debugger/reference/idebugclassfield-enumconstructors.md)|创建此类的构造函数的枚举器。|
|[GetDefaultIndexer](../../../extensibility/debugger/reference/idebugclassfield-getdefaultindexer.md)|获取默认索引器的名称。|
|[EnumNestedEnums](../../../extensibility/debugger/reference/idebugclassfield-enumnestedenums.md)|创建此类的嵌套枚举器的枚举器。|

## <a name="requirements"></a>要求
 标头： sh.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)