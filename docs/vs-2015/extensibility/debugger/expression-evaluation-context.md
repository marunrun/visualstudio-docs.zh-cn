---
title: 表达式计算上下文 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, context
ms.assetid: a2fd3758-09bd-45ae-8ecc-2d276c0036ba
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 377609cb9f971b667872c198a53b45a6288f2c15
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152782"
---
# <a name="expression-evaluation-context"></a>表达式计算上下文
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 调试中， **表达式计算上下文**：  
  
- 表示表达式计算的上下文。 通常，计算上下文对应于要在其中计算变量、参数、函数和方法的词法范围。 例如，与堆栈帧关联的表达式求值上下文将提供用于计算本地变量、方法参数和类成员的上下文 (如果适用) 。  
  
- 当程序在断点处停止时存在。 表达式本身是一个数据结构，它表示可在给定上下文中进行绑定和计算的已分析表达式。  
  
     更详细地介绍了使用 [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 方法创建的表达式。 计算表达式时，它将生成一个可打印字符串，其中包含变量或参数的名称和类型及其值。 此字符串将显示在监视窗口或 IDE 的 "局部变量" 窗口中。  
  
     给定一个 `BSTR` 和一个 [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) 接口，调试引擎 (DE) 可以通过分析表达式来创建 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 接口。 给定 `IDebugExpression2` 接口，DE 可以通过同步或异步表达式计算获得值。 此值与变量或参数的名称和类型一起发送到 IDE 以显示。  
  
## <a name="see-also"></a>另请参阅  
 [表达式计算接口](../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [调试器上下文](../../extensibility/debugger/debugger-contexts.md)
