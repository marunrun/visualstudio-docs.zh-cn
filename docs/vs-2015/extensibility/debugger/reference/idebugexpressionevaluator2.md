---
title: IDebugExpressionEvaluator2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugExpressionEvaluator2 interface
ms.assetid: cebe649f-1c77-4d33-854f-30d4f00eceb4
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 840f9be067d591b27bda6a01b6469699524787d1
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63426439"
---
# <a name="idebugexpressionevaluator2"></a>IDebugExpressionEvaluator2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 表示的表达式计算器 (EE) 的增强的版本。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugExpressionEvaluator2 : IDebugExpressionEvaluator  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 此接口由表达式计算器实现。  
  
## <a name="methods"></a>方法  
 除了上的方法[IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)接口，此接口实现以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[GetService](../../../extensibility/debugger/reference/idebugexpressionevaluator2-getservice.md)|检索服务对象给出它的唯一标识符。|  
|[PreloadModules](../../../extensibility/debugger/reference/idebugexpressionevaluator2-preloadmodules.md)|预加载指定的符号提供程序指定的模块。|  
|[SetCallback](../../../extensibility/debugger/reference/idebugexpressionevaluator2-setcallback.md)|使表达式计算器 (EE) 来指定调试器引擎 (DE) 将用于读取指标设置回调接口。|  
|[SetCorPath](../../../extensibility/debugger/reference/idebugexpressionevaluator2-setcorpath.md)|公共语言运行时 (CLR) 加载在调试器中设置的路径。|  
|[SetIDebugIDECallback](../../../extensibility/debugger/reference/idebugexpressionevaluator2-setidebugidecallback.md)|允许在初始化期间向表达式计算器传递回调调试引擎。|  
|[Terminate](../../../extensibility/debugger/reference/idebugexpressionevaluator2-terminate.md)|停止并清除表达式计算器。|  
  
## <a name="requirements"></a>要求  
 标头：Ee.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
