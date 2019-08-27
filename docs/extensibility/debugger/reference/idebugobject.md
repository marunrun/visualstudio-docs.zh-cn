---
title: IDebugObject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject
helpviewer_keywords:
- IDebugObject interface
ms.assetid: 05cd8bf4-c9ee-4b49-b782-2263c33067d6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 97fd6c328b15c8e41dbbc2b4e45bfc4285b4273f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66319030"
---
# <a name="idebugobject"></a>IDebugObject
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口表示联编程序创建要封装的符号和表达式的值的对象。

## <a name="syntax"></a>语法

```
IDebugObject : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 表达式计算器实现此接口表示的对象。

## <a name="notes-for-callers"></a>调用方的说明
 此接口是表达式计算器分析表达式中使用的所有对象的基类。 返回通过调用[绑定](../../../extensibility/debugger/reference/idebugbinder-bind.md)方法。 [QueryInterface](/cpp/atl/queryinterface)从此接口获取更多专用的接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugObject`。

|方法|描述|
|------------|-----------------|
|[GetSize](../../../extensibility/debugger/reference/idebugobject-getsize.md)|获取对象的大小。|
|[GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)|获取对象的值作为一系列连续的字节数。|
|[SetValue](../../../extensibility/debugger/reference/idebugobject-setvalue.md)|设置对象的值从一系列连续的字节数。|
|[SetReferenceValue](../../../extensibility/debugger/reference/idebugobject-setreferencevalue.md)|设置此对象的引用值。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugobject-getmemorycontext.md)|获取表示对象的值的地址的内存上下文。|
|[GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)|调试引擎的地址空间中创建托管对象的副本。|
|[IsNullReference](../../../extensibility/debugger/reference/idebugobject-isnullreference.md)|测试此对象是否为 null 引用。|
|[IsEqual](../../../extensibility/debugger/reference/idebugobject-isequal.md)|与此对象进行比较。|
|[IsReadOnly](../../../extensibility/debugger/reference/idebugobject-isreadonly.md)|确定此对象是只读的。|
|[IsProxy](../../../extensibility/debugger/reference/idebugobject-isproxy.md)|确定对象是否透明代理。|

## <a name="remarks"></a>备注
 表达式计算器使用此接口作为基类，用于表示分析树中的对象。

## <a name="requirements"></a>要求
 标头： ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)
- [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)