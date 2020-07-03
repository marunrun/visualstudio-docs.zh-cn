---
title: DA0007 - 避免使用控制流异常 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.rules.DAExceptionsThrown
- vs.performance.7
- vs.performance.rules.DA0007
- vs.performance.DA0007
ms.assetid: ee8ba8b5-2313-46c9-b129-3f3a2a232898
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: a33d5b8d18f18fb6bf7a2420603d994d845ce8f2
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520791"
---
# <a name="da0007-avoid-using-exceptions-for-control-flow"></a>DA0007：避免使用控制流异常

|项|“值”|
|-|-|
|规则 ID|DA0007|
|类别|.NET Framework 使用情况|
|分析方法|全部|
|消息|持续引发大量异常。 请考虑减少使用程序逻辑中的异常。|
|消息类型|警告|

 使用采样法、.NET 内存或资源争用方法进行分析时，必须至少收集 25 个样本才能触发此规则。

## <a name="cause"></a>原因
 分析数据中调用了速率较高的 .NET Framework 异常处理程序。 请考虑使用其他控制流逻辑，以便减少引发的异常数。

## <a name="rule-description"></a>规则说明
 虽然使用异常处理程序捕获错误和中断程序执行的其他事件是一个好的做法，但在常规程序执行逻辑中使用异常处理程序成本很高，应当避免。 大多数情况下，异常应仅用于不经常出现且意外的情况。 异常不应用于在典型程序流中返回值。 在许多情况下，可以验证值和使用条件逻辑来暂停执行引起问题的语句，从而避免引发异常。

 有关详细信息，请参阅 MSDN 上 Microsoft 模式和做法库“提高 .NET 应用程序性能和可扩展性”卷中第 5 章 - 提高托管代码性能”的[异常管理](/previous-versions/msp-n-p/ff647790(v=pandp.10)#exception-management)部分  。

## <a name="how-to-investigate-a-warning"></a>如何调查警告
 双击“错误列表”窗口中的消息，导航到“标记”视图。 查找包含 .NET CLR Exceptions(@ProcessInstance)\\# of Excels Thrown / sec 度量的列。 确定是否存在异常处理更频繁的程序执行特定阶段。 使用采样分析，尝试标识生成频繁异常的 throw 语句和 try/catch 块。 如有必要，请向 catch 块添加逻辑，以便了解处理最频繁的异常。 如有可能，使用简单的流控制逻辑或验证代码替换频繁执行的 throw 语句或 catch 块。

 例如，如果发现应用程序正在处理频繁的 DivideByZeroException 异常，则向程序添加逻辑以便检查为零值的分母将改进应用程序的性能。
