---
title: DA0012 - 大量反射 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.rules.DAReflection
- vs.performance.12
- vs.performance.rules.DA0012
- vs.performance.DA0011
ms.assetid: c92a1d76-21fa-426e-8b1b-a3c08e9bcbca
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: df8b9c80b3d3b12cb556947a7ca77b3141fb853d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520636"
---
# <a name="da0012-significant-amount-of-reflection"></a>DA0012：大量反射

|项|“值”|
|-|-|
|规则 ID|DA0012|
|类别|.NET Framework 使用情况|
|分析方法|采样|
|消息|当前可能存在过度反射。 这是成本较高的操作。|
|规则类型|警告|

## <a name="cause"></a>原因
 对 System.Reflection 方法（如 InvokeMember 和 GetMember）或 Type 方法（如 MemberInvoke）的调用是分析数据的重要组成部分。 如果可能，请考虑用对依赖程序集方法的早期绑定来替代这些方法。

## <a name="rule-description"></a>规则说明
 反射是 .NET framework 的一项灵活功能，可用于将应用程序后期绑定到依赖的运行时程序集，或在运行时期间创建并动态执行新类型。 但是，频繁使用或紧凑循环地调用这些技术则可导致性能降低。

 有关详细信息，请参阅 MSDN 上 Microsoft 模式和做法库“提高 .NET 应用程序性能和可扩展性”卷中“第 5 章 - 提高托管代码性能”的 [Reflection and Late Binding](/previous-versions/msp-n-p/ff647790(v=pandp.10)#reflection-and-late-binding)（反射和后期绑定）部分。

## <a name="how-to-investigate-a-warning"></a>如何调查警告
 双击“错误列表”窗口中的消息，导航到分析数据的[函数详细信息视图](../profiling/function-details-view.md)。 检查 System.Type 或 System.Reflection 方法的调用函数，以查找程序中使用 .NET Reflection API 最频繁的部分。 避免使用返回元数据的方法。 当应用程序的性能十分重要时，可能需要避免在运行时使用后期绑定或动态创建类型。
