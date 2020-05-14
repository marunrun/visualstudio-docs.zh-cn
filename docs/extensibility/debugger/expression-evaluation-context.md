---
title: 表达式计算上下文 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, context
ms.assetid: a2fd3758-09bd-45ae-8ecc-2d276c0036ba
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e939a4fa5f4673e2f701206c96599c54bc0c3b51
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738733"
---
# <a name="expression-evaluation-context"></a>表达式计算上下文
在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试中，**表达式计算上下文**：

- 表示表达式计算的上下文。 通常，计算上下文对应于计算变量、参数、函数和方法的词法范围。 例如，与堆栈框架关联的表达式计算上下文将提供用于评估局部变量、方法参数和类成员（如果适用）的上下文。

- 当程序在断点停止时存在。 表达式本身是一个数据结构，表示可准备在给定上下文中绑定和评估的解析表达式。

     有关详细信息，将使用[ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)方法创建表达式。 计算表达式时，它生成一个可打印的字符串，其中包含变量或参数的名称和类型及其值。 此字符串显示在"监视"窗口或 IDE 的"局部变量"窗口中。

     给定`BSTR`和[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口，调试引擎 （DE） 可以通过分析表达式创建[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)接口。 给定接口`IDebugExpression2`，DE 可以通过同步或异步表达式计算获取值。 此值以及变量或参数的名称和类型将发送到 IDE 进行显示。

## <a name="see-also"></a>请参阅
- [表达式评估接口](../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)
