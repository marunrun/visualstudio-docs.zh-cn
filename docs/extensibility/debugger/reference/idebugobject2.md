---
title: IDebugObject2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2
helpviewer_keywords:
- IDebugObject2 interface
ms.assetid: ef640967-8adb-4793-994d-ae1736510891
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e468b5a282ffb5466d57a3c9b1a37aa3ae8643ed
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726072"
---
# <a name="idebugobject2"></a>IDebugObject2
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口提供有关对象的其他信息。

## <a name="syntax"></a>语法

```
IDebugObject2 : IDebugObject
```

## <a name="notes-for-implementers"></a>实施者说明
 表达式赋值器实现此接口，以支持别名和对对象信息的访问。

## <a name="notes-for-callers"></a>呼叫者备注
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口可以使用[查询接口](/cpp/atl/queryinterface)获取此接口。 此外[，GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md)返回此接口。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法
 除了[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口上的方法外，`IDebugObject2`该接口还实现了以下功能：

|方法|描述|
|------------|-----------------|
|[GetBackingFieldForProperty](../../../extensibility/debugger/reference/idebugobject2-getbackingfieldforproperty.md)|获取可能支持此对象表示的属性的字段或变量（如果有）。|
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugobject2-geticordebugvalue.md)|获取表示此对象值的托管代码对象。|
|[CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)|为此对象创建唯一 ID 或返回现有别名。|
|[获取别名](../../../extensibility/debugger/reference/idebugobject2-getalias.md)|获取与此对象关联的别名（如果有）。|
|[GetField](../../../extensibility/debugger/reference/idebugobject2-getfield.md)|获取此对象的类型。|
|[IsUserData](../../../extensibility/debugger/reference/idebugobject2-isuserdata.md)|确定此对象是否表示用户数据。|
|[IsEncOutdated](../../../extensibility/debugger/reference/idebugobject2-isencoutdated.md)|确定"编辑"和"继续"状态是否不再有效。<br /><br /> 自定义表达式赋值器不实现此方法（应始终返回`E_NOTIMPL`）。|

## <a name="remarks"></a>备注
 有关别名的讨论，请参阅[IDebugAlias。](../../../extensibility/debugger/reference/idebugalias.md)

## <a name="requirements"></a>要求
 标题： ee.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
- [获取对象](../../../extensibility/debugger/reference/idebugalias-getobject.md)
