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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68152782"
---
# <a name="expression-evaluation-context"></a>表达式计算上下文
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在中[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]调试**表达式计算上下文**:  
  
- 表示为表达式计算上下文。 通常情况下，评估上下文对应于在其中计算变量、 参数、 函数和方法的词法范围。 例如，表达式评估上下文与堆栈帧关联将用于评估本地变量、 方法参数和类成员 （如果适用） 提供的上下文。  
  
- 当程序已停止在断点处存在。 该表达式本身是一种数据结构，表示已准备好绑定和评估给定上下文中的已分析的表达式。  
  
     在更多详细信息，使用创建表达式[ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)方法。 当计算表达式时，它生成一个包含名称和类型的变量或参数，并且其值的可打印字符串。 在监视窗口中或在 IDE 的局部变量窗口中显示此字符串。  
  
     给定`BSTR`和一个[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口，可以创建调试引擎 (DE) [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)接口通过分析表达式。 给定`IDebugExpression2`接口，DE 可以获取通过同步或异步表达式计算的值。 此值，以及名称和类型的变量或参数，用于显示发送到 IDE。  
  
## <a name="see-also"></a>请参阅  
 [表达式计算接口](../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [调试器上下文](../../extensibility/debugger/debugger-contexts.md)
