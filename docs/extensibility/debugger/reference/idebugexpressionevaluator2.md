---
title: IDebugExpressionEvaluator2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugExpressionEvaluator2 interface
ms.assetid: cebe649f-1c77-4d33-854f-30d4f00eceb4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7041456bf0f3ae7930a73399d43dbf7cac6b3b32
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80729139"
---
# <a name="idebugexpressionevaluator2"></a>IDebugExpressionEvaluator2
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表示表达式计算器 (EE) 的增强版本。

## <a name="syntax"></a>语法

```
IDebugExpressionEvaluator2 : IDebugExpressionEvaluator
```

## <a name="notes-for-implementers"></a>实施者注意事项
 此接口由表达式计算器实现。

## <a name="methods"></a>方法
 除了 [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md) 接口上的方法，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetService](../../../extensibility/debugger/reference/idebugexpressionevaluator2-getservice.md)|根据给定的唯一标识符检索服务对象。|
|[PreloadModules](../../../extensibility/debugger/reference/idebugexpressionevaluator2-preloadmodules.md)|预加载指定的符号提供程序指定的模块。|
|[SetCallback](../../../extensibility/debugger/reference/idebugexpressionevaluator2-setcallback.md)|使表达式计算器 (EE) 指定 (DE) 将用于读取指标设置的回调接口。|
|[SetCorPath](../../../extensibility/debugger/reference/idebugexpressionevaluator2-setcorpath.md)|设置 (CLR) 加载到调试器中的公共语言运行时的路径。|
|[SetIDebugIDECallback](../../../extensibility/debugger/reference/idebugexpressionevaluator2-setidebugidecallback.md)|使调试引擎能够在初始化期间向表达式计算器传递回调。|
|Terminate|停止并清除表达式计算器。|

## <a name="requirements"></a>要求
 标头： Ee。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
