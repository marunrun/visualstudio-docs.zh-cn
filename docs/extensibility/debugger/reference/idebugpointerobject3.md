---
title: IDebugPointerObject3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPointerObject3 interface
ms.assetid: 11d26af4-1079-435e-96fa-d5269cbea8eb
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 85f1962b1a9d9d8b8c9d2fe6b8e7699d6561b67d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66343771"
---
# <a name="idebugpointerobject3"></a>IDebugPointerObject3
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表示在分析树中，指针并扩展**IDebugPointerObject**接口。

## <a name="syntax"></a>语法

```
IDebugPointerObject3 : IDebugPointerObject
```

## <a name="notes-for-implementers"></a>实施者的说明
 表达式计算器 (EE) 实现此接口。

## <a name="methods"></a>方法
 除了上的方法[IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)接口，此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[GetPointerAddress](../../../extensibility/debugger/reference/idebugpointerobject3-getpointeraddress.md)|检索指针的地址。|

## <a name="requirements"></a>要求
 标头：Ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll