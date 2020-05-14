---
title: IDebugObject |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject
helpviewer_keywords:
- IDebugObject interface
ms.assetid: 05cd8bf4-c9ee-4b49-b782-2263c33067d6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6801176964a47646f03091131e1be89cf63c97f8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726311"
---
# <a name="idebugobject"></a>IDebugObject
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口表示活页夹为封装符号和表达式的值而创建的对象。

## <a name="syntax"></a>语法

```
IDebugObject : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 表达式赋值器实现此接口以表示对象。

## <a name="notes-for-callers"></a>呼叫者备注
 此接口是表达式赋值器在解析表达式中使用的所有对象的基类。 它通过调用[Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)方法返回。 [查询接口](/cpp/atl/queryinterface)从此接口获取更专业的接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugObject`。

|方法|描述|
|------------|-----------------|
|[GetSize](../../../extensibility/debugger/reference/idebugobject-getsize.md)|获取对象的大小。|
|[GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)|获取对象的值作为连续字节系列。|
|[SetValue](../../../extensibility/debugger/reference/idebugobject-setvalue.md)|设置连续字节序列中对象的值。|
|[SetReferenceValue](../../../extensibility/debugger/reference/idebugobject-setreferencevalue.md)|设置此对象的引用值。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugobject-getmemorycontext.md)|获取表示对象值地址的内存上下文。|
|[GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)|在调试引擎的地址空间中创建托管对象的副本。|
|[IsNullReference](../../../extensibility/debugger/reference/idebugobject-isnullreference.md)|测试此对象是否为空引用。|
|[IsEqual](../../../extensibility/debugger/reference/idebugobject-isequal.md)|将对象与此对象进行比较。|
|[仅阅读](../../../extensibility/debugger/reference/idebugobject-isreadonly.md)|确定此对象是否为只读对象。|
|[IsProxy](../../../extensibility/debugger/reference/idebugobject-isproxy.md)|确定对象是否为透明代理。|

## <a name="remarks"></a>备注
 表达式赋值器使用此接口作为基类来表示解析树中的对象。

## <a name="requirements"></a>要求
 标题： ee.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)
- [绑定](../../../extensibility/debugger/reference/idebugbinder-bind.md)
