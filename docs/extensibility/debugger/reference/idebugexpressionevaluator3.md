---
title: IDebugExpressionEvaluator3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugExpressionEvaluator3 interface
ms.assetid: c27c2a14-300b-4535-be22-767c83602f69
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7d00f24505de763d85d4d454d6f3bde459653689
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352732"
---
# <a name="idebugexpressionevaluator3"></a>IDebugExpressionEvaluator3
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 增强型的分析器目录树表示的表达式计算器 (EE)。

## <a name="syntax"></a>语法

```
IDebugExpressionEvaluator3 : IDebugExpressionEvaluator2
```

## <a name="notes-for-callers"></a>调用方的说明
 此版本的分析器将传递符号提供程序和评估的帧的地址。

## <a name="methods"></a>方法
 除了上的方法[IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)接口，此接口实现了以下方法：

|方法|描述|
|------------|-----------------|
|[Parse2](../../../extensibility/debugger/reference/idebugexpressionevaluator3-parse2.md)|将一个表达式字符串转换为给定的符号提供程序和评估的帧的地址的已分析表达式。|

## <a name="requirements"></a>要求
 标头：Ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll