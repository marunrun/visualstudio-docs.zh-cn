---
title: IDebugObject2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2
helpviewer_keywords:
- IDebugObject2 interface
ms.assetid: ef640967-8adb-4793-994d-ae1736510891
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d3f027fd08c38433d5f1357e56d90df96e223854
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66317252"
---
# <a name="idebugobject2"></a>IDebugObject2
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口提供的对象有关的其他信息。

## <a name="syntax"></a>语法

```
IDebugObject2 : IDebugObject
```

## <a name="notes-for-implementers"></a>实施者的说明
 表达式计算器实现此接口以提供支持的别名和访问对象有关的信息。

## <a name="notes-for-callers"></a>调用方的说明
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口可以获取此接口通过[QueryInterface](/cpp/atl/queryinterface)。 此外， [GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md)返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了上的方法[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口，`IDebugObject2`接口实现了以下：

|方法|描述|
|------------|-----------------|
|[GetBackingFieldForProperty](../../../extensibility/debugger/reference/idebugobject2-getbackingfieldforproperty.md)|获取字段或变量 （如果有），可能会支持此对象表示的属性。|
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugobject2-geticordebugvalue.md)|获取表示此对象的值的托管的代码对象。|
|[CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)|创建此对象的唯一 ID，或返回现有别名。|
|[GetAlias](../../../extensibility/debugger/reference/idebugobject2-getalias.md)|如果有，获取与此对象相关联的别名。|
|[GetField](../../../extensibility/debugger/reference/idebugobject2-getfield.md)|获取此对象的类型。|
|[IsUserData](../../../extensibility/debugger/reference/idebugobject2-isuserdata.md)|确定此对象是否表示用户数据。|
|[IsEncOutdated](../../../extensibility/debugger/reference/idebugobject2-isencoutdated.md)|确定是否编辑并继续状态将不再有效。<br /><br /> 自定义表达式计算器不实现此方法 (它应始终返回`E_NOTIMPL`)。|

## <a name="remarks"></a>备注
 请参阅[IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)有关别名的讨论。

## <a name="requirements"></a>要求
 标头： ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
- [GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md)