---
title: IDebug属性2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2
helpviewer_keywords:
- IDebugProperty2 interface
ms.assetid: a7d5c70f-a1a5-4120-9f70-184e01c25bff
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4b04abdac135143ccbbd1b8e5632bf85c974f29d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721222"
---
# <a name="idebugproperty2"></a>IDebugProperty2
此接口表示堆栈帧属性、程序文档属性或其他属性。 该属性通常是表达式计算的结果。

> [!NOTE]
> 不应将"属性"的这种使用与类的成员变量的含义混淆，尽管 可以`IDebugProperty2`表示此类实体。

## <a name="syntax"></a>语法

```
IDebugProperty2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 DE 实现此接口以表示特定类型的值。 例如，该值可以是表达式计算的结果、用于显示内存的内存上下文或寄存器及其值的列表。

## <a name="notes-for-callers"></a>呼叫者备注
 调用[评估同步](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)[或评估同步](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)以获取此接口，该接口表示评估的结果。 `IDebugExpression2::EvaluateAsync`通过向 SDM 发送[IDebugExpressionExpression评估完成事件2 接口](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)来返回此接口，SDM 又调用[GetResult](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)来检索该属性。

- [GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertycreateevent2-getdebugproperty.md)返回此接口以提供关联的脚本文档。

- [GetReturnValue](../../../extensibility/debugger/reference/idebugreturnvalueevent2-getreturnvalue.md)返回此接口以表示函数的返回值。

- [GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md)返回此接口以表示程序的各种属性，如名称或内存上下文。

- [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)返回此接口以表示堆栈帧的各种属性，如局部变量。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugProperty2`。

|方法|描述|
|------------|-----------------|
|[获取财产信息](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)|填写描述属性[的DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构。|
|[SetValueAsString](../../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)|从字符串设置属性的值。|
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugproperty2-setvalueasreference.md)|从给定引用的值设置属性的值。|
|[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)|枚举属性的子级。|
|[GetParent](../../../extensibility/debugger/reference/idebugproperty2-getparent.md)|返回属性的父级。|
|[GetDerivedMostProperty](../../../extensibility/debugger/reference/idebugproperty2-getderivedmostproperty.md)|返回描述属性最派生属性的属性。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)|返回组成属性值的内存字节。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)|返回属性值的内存上下文。|
|[GetSize](../../../extensibility/debugger/reference/idebugproperty2-getsize.md)|返回属性值的大小（以字节为单位）。|
|[获取参考](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)|返回对此属性值的引用。|
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugproperty2-getextendedinfo.md)|返回属性的扩展信息。|

## <a name="remarks"></a>备注
 属性（由`IDebugProperty2`接口表示）可以视为具有名称、类型和地址的值。 更笼统地说，`IDebugProperty2`可以表示具有层次结构的任何内容，以及父节点和子节点。

 属性通常是短暂的，仅持续于当前堆栈帧（例如）。 另一方面，引用（由[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)接口表示）只要该值保留在内存中，该引用就持续。

 IDE 可以使用该`IDebugProperty2`接口允许用户在运行时浏览和修改属性。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
