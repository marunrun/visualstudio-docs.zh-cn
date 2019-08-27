---
title: IDebugPropertyField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPropertyField
helpviewer_keywords:
- IDebugPropertyField interface
ms.assetid: b50edb2c-fb8d-4def-993d-17d23d2027c1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ecaf93a563627306b9fd1ab2e3adad0a83b412ab
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322713"
---
# <a name="idebugpropertyfield"></a>IDebugPropertyField
此接口提供允许获取和设置属性的函数。

## <a name="syntax"></a>语法

```
IDebugPropertyField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>实施者的说明
 符号提供程序实现此接口上实现的相同对象[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)。 此接口是支持属性的概念的类的专用化。

## <a name="notes-for-callers"></a>调用方的说明
 使用[QueryInterface](/cpp/atl/queryinterface)若要获取此接口从[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)方法将返回`FIELD_KIND_PROP`。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了上的方法[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)并[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口，此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[GetPropertyGetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md)|获取获取的属性的方法。|
|[GetPropertySetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertysetter.md)|获取设置的属性的方法。|

## <a name="remarks"></a>备注
 属性是一个托管的代码的概念，表示视为变量的方法。 属性不存在于非托管C++。

## <a name="requirements"></a>要求
 标头： sh.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)