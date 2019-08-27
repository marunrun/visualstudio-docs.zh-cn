---
title: IEnumDebugObjects | Microsoft Docs
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
ms.openlocfilehash: dea4b4781fd8026c29436bbd37a6bfa6824e73b3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66339484"
---
# <a name="ienumdebugobjects"></a>IEnumDebugObjects
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口表示的对象实现的集合[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口。

## <a name="syntax"></a>语法

```
IEnumDebugObjects : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 表达式计算器实现此接口可提供的实现的对象集[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口。 请注意，这不是由于存在一个标准 COM 枚举[GetCount](../../../extensibility/debugger/reference/ienumdebugobjects-getcount.md)方法。

## <a name="notes-for-callers"></a>调用方的说明
- [GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 此接口实现以下方法。

|方法|描述|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugobjects-next.md)|检索下一套[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)枚举中的对象。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugobjects-skip.md)|将跳过指定的数目的条目。|
|[Reset](../../../extensibility/debugger/reference/ienumdebugobjects-reset.md)|将枚举重置为第一个条目。|
|[Clone](../../../extensibility/debugger/reference/ienumdebugobjects-clone.md)|检索当前枚举的副本。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugobjects-getcount.md)|检索枚举中的条目数。|

## <a name="remarks"></a>备注
 此接口允许对一的数组中的对象进行枚举的调试引擎。

## <a name="requirements"></a>要求
 标头： ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)