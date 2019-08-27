---
title: IDebugFunctionObject2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2 interface
ms.assetid: 56b2fdff-146d-4138-a34c-59a9c65a3ddd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e231029fb37607464f5e183d531cad9ee5004a73
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66313382"
---
# <a name="idebugfunctionobject2"></a>IDebugFunctionObject2
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表示一个函数，并增强[IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)接口。

## <a name="syntax"></a>语法

```
IDebugFunctionObject2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 表达式计算器 (EE) 实现此接口来表示一个函数。

## <a name="notes-for-callers"></a>调用方的说明
 此接口的方法将延迟的那些**IDebugFunctionObject**以下方面：

- **IDebugEvaluate**方法采用标志。

- **CreateObject**方法采用标志和超时。

- **CreateStringObjectWithLength**方法采用一个长度。

## <a name="methods"></a>方法
 此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject2-createobject.md)|创建使用给定评估标志设置和超时值的构造函数的对象。|
|[CreateStringObjectWithLength](../../../extensibility/debugger/reference/idebugfunctionobject2-createstringobjectwithlength.md)|创建具有指定的长度的字符串对象。|
|[Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject2-evaluate.md)|调用函数，并返回结果值作为对象。|

## <a name="requirements"></a>要求
 标头：Ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll