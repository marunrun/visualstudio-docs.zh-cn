---
title: IDebugPointer对象 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject
helpviewer_keywords:
- IDebugPointerObject interface
ms.assetid: 257fa167-b46e-4ffb-9a12-272efbf26702
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4b28189b3f0a07a27f5e4478f64963a63d634db5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725486"
---
# <a name="idebugpointerobject"></a>IDebugPointerObject
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口表示指针对象。

## <a name="syntax"></a>语法

```
IDebugPointerObject : IDebugObject
```

## <a name="notes-for-implementers"></a>实施者说明
 表达式赋值器实现此接口以表示指针对象。

## <a name="notes-for-callers"></a>呼叫者备注
 如果表示指针，`IDebugObject`[则 IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口可以使用[查询接口](/cpp/atl/queryinterface)获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了从[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)继承的方法外，`IDebugPointerObject`接口还公开了以下方法。

|方法|描述|
|------------|-----------------|
|[Dereference](../../../extensibility/debugger/reference/idebugpointerobject-dereference.md)|获取接口指向的对象。|
|[GetBytes](../../../extensibility/debugger/reference/idebugpointerobject-getbytes.md)|获取接口指向的值，作为一系列连续字节。|
|[设置字节](../../../extensibility/debugger/reference/idebugpointerobject-setbytes.md)|设置接口从一系列连续字节指向的值。|

## <a name="remarks"></a>备注
 表达式赋值器使用此接口表示解析树中的指针。

## <a name="requirements"></a>要求
 标题： ee.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
