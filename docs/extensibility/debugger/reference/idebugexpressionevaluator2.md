---
title: IDebug表达式评估器2 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729139"
---
# <a name="idebugexpressionevaluator2"></a>IDebugExpressionEvaluator2
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表示表达式赋值器 （EE） 的增强版本。

## <a name="syntax"></a>语法

```
IDebugExpressionEvaluator2 : IDebugExpressionEvaluator
```

## <a name="notes-for-implementers"></a>实施者说明
 此接口由表达式赋值器实现。

## <a name="methods"></a>方法
 除了[IDebugExpression 评估器](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)接口上的方法外，此接口还实现了以下方法：

|方法|描述|
|------------|-----------------|
|[获取服务](../../../extensibility/debugger/reference/idebugexpressionevaluator2-getservice.md)|检索给定其唯一标识符的服务对象。|
|[PreloadModules](../../../extensibility/debugger/reference/idebugexpressionevaluator2-preloadmodules.md)|预加载指定符号提供程序指定的模块。|
|[SetCallback](../../../extensibility/debugger/reference/idebugexpressionevaluator2-setcallback.md)|使表达式赋值器 （EE） 指定调试器引擎 （DE） 将用于读取指标设置的回调接口。|
|[SetCorPath](../../../extensibility/debugger/reference/idebugexpressionevaluator2-setcorpath.md)|设置调试器中加载的通用语言运行时 （CLR） 的路径。|
|[SetIDebugIDECallback](../../../extensibility/debugger/reference/idebugexpressionevaluator2-setidebugidecallback.md)|使调试引擎能够在初始化期间将回调传递给表达式赋值器。|
|[终止](../../../extensibility/debugger/reference/idebugexpressionevaluator2-terminate.md)|停止并清理表达式赋值器。|

## <a name="requirements"></a>要求
 标题： Ee.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll
