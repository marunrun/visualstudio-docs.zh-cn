---
title: IEnumDebugObjects |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugObjects
helpviewer_keywords:
- IEnumDebugObjects interface
ms.assetid: 0950364c-6c8a-4b6c-ba37-c6aa359fa72c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 749b3faf938fbc862fdf9b406127c898ee6b6d98
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72727560"
---
# <a name="ienumdebugobjects"></a>IEnumDebugObjects
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅[Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口表示实现[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口的对象的集合。

## <a name="syntax"></a>语法

```
IEnumDebugObjects : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 表达式计算器实现此接口以提供实现[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口的对象集。 请注意，这不是标准的 COM 枚举，因为存在[GetCount](../../../extensibility/debugger/reference/ienumdebugobjects-getcount.md)方法。

## <a name="notes-for-callers"></a>调用方说明
- [GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法
 此接口实现以下方法。

|方法|描述|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugobjects-next.md)|从枚举中检索下一组[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)对象。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugobjects-skip.md)|跳过指定数量的条目。|
|[Reset](../../../extensibility/debugger/reference/ienumdebugobjects-reset.md)|将枚举重置为第一个条目。|
|[Clone](../../../extensibility/debugger/reference/ienumdebugobjects-clone.md)|检索当前枚举的副本。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugobjects-getcount.md)|检索枚举中的项数。|

## <a name="remarks"></a>备注
 此接口允许调试引擎枚举数组中的一组对象。

## <a name="requirements"></a>要求
 标头： ee。h

 命名空间： VisualStudio

 程序集： VisualStudio。

## <a name="see-also"></a>请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)