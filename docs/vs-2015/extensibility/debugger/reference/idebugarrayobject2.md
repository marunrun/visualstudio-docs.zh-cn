---
title: IDebugArrayObject2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugArrayObject2 interface
ms.assetid: be6e504d-4ab3-4141-a61b-0953ee0e038e
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d68b0db20150bd81a9b2b4aef29c78701a6bc8ee
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440692"
---
# <a name="idebugarrayobject2"></a>IDebugArrayObject2
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表示一个托管的数组对象，并允许的表达式计算器 (EE) 来确定数组的基索引 （下限）。

## <a name="syntax"></a>语法

```
IDebugArrayObject2 : IDebugArrayObject
```

## <a name="notes-for-implementers"></a>实施者的说明
 这一点被通过托管的调试引擎 (DE)。

## <a name="methods"></a>方法
 除了上的方法[IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)接口，此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[GetBaseIndices](../../../extensibility/debugger/reference/idebugarrayobject2-getbaseindices.md)|检索给定数组中的维度数的每个索引 （下限） 的基索引。|
|[HasBaseIndices](../../../extensibility/debugger/reference/idebugarrayobject2-hasbaseindices.md)|确定数组是否具有基本索引 （下限） 定义。|

## <a name="remarks"></a>备注
 表达式计算器使用此接口来表示分析树中的托管的数组。

## <a name="requirements"></a>要求
 标头：Ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll