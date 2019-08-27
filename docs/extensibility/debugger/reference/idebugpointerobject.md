---
title: IDebugPointerObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject
helpviewer_keywords:
- IDebugPointerObject interface
ms.assetid: 257fa167-b46e-4ffb-9a12-272efbf26702
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c884f2794031d92add956bf4364824165ee1edfb
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66343930"
---
# <a name="idebugpointerobject"></a>IDebugPointerObject
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口表示的指针对象。

## <a name="syntax"></a>语法

```
IDebugPointerObject : IDebugObject
```

## <a name="notes-for-implementers"></a>实施者的说明
 表达式计算器实现此接口来表示指针对象。

## <a name="notes-for-callers"></a>调用方的说明
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口可以获取此接口通过[QueryInterface](/cpp/atl/queryinterface)如果`IDebugObject`表示的指针。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了继承的方法之外[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)，则`IDebugPointerObject`接口公开以下方法。

|方法|描述|
|------------|-----------------|
|[Dereference](../../../extensibility/debugger/reference/idebugpointerobject-dereference.md)|获取该接口所指向的对象。|
|[GetBytes](../../../extensibility/debugger/reference/idebugpointerobject-getbytes.md)|获取该接口指向作为一系列连续字节的值。|
|[SetBytes](../../../extensibility/debugger/reference/idebugpointerobject-setbytes.md)|设置该接口指向一系列连续字节中的值。|

## <a name="remarks"></a>备注
 表达式计算器使用此接口来表示分析树中的指针。

## <a name="requirements"></a>要求
 标头： ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)