---
title: IDebugArrayObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject
helpviewer_keywords:
- IDebugArrayObject method
ms.assetid: a1c8e77e-dee1-4748-a516-6ab032a8f54f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 709273b89d89759163acb725220d1092d33ad72f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80736210"
---
# <a name="idebugarrayobject"></a>IDebugArrayObject
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口表示数组对象。

## <a name="syntax"></a>语法

```
IDebugArrayObject : IDebugObject
```

## <a name="notes-for-implementers"></a>实施者注意事项
 表达式计算器实现此接口来表示数组。

## <a name="notes-for-callers"></a>调用方说明
 如果对象表示一个数组，则 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 接口可以使用 [QueryInterface](/cpp/atl/queryinterface) 获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了接口上的方法之外 `IDebugObject` ，还会在接口上实现以下方法 `IDebugArrayObject` 。

|方法|说明|
|------------|-----------------|
|[GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md)|获取数组中元素的计数。|
|[GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)|获取数组的元素。|
|[GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)|获取数组的所有元素。|
|[GetRank](../../../extensibility/debugger/reference/idebugarrayobject-getrank.md)|获取数组的秩。|
|[GetDimensions](../../../extensibility/debugger/reference/idebugarrayobject-getdimensions.md)|获取数组的尺寸。|

## <a name="remarks"></a>备注
 表达式计算器使用此接口来表示分析树中的数组。

## <a name="requirements"></a>要求
 标头： ee。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
