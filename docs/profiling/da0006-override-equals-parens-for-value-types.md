---
title: DA0006：替代值类型的 Equals() | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.rules.DAOverrideEquals
- vs.performance.6
- vs.performance.DA0006
- vs.performance.rules.DA0006
ms.assetid: 4d85bdd6-b571-47e0-afd6-ba3764e4eed5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 805fa62b003559eb92c0531b0f4df7133cf0cdf5
ms.sourcegitcommit: 257fc60eb01fefafa9185fca28727ded81b8bca9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72911993"
---
# <a name="da0006-override-equals-for-value-types"></a>DA0006：替代值类型的 Equals()

|||
|-|-|
|规则 ID|DA0006|
|类别|.NET Framework 使用情况|
|分析方法|采样|
|消息|替代值类型上的 Equals 和相等运算符。|
|消息类型|警告|

## <a name="cause"></a>原因
 对 Equals 方法或公共值类型的相等运算符的调用在分析数据中占很大比例。 请考虑实施更有效的方法。

## <a name="rule-description"></a>规则说明
 对于值类型，Equals 的继承的实现使用 <xref:System.Reflection> 库，并比较类型中所有字段的内容。 反射需要消耗大量计算资源，可能没有必要比较每一个字段是否相等。 如果希望用户对实例进行比较或排序，或者希望用户将它们用作哈希表键，则值类型应实现 Equals。 如果编程语言支持运算符重载，则还应提供相等和不等运算符的实现。

 有关如何重写 Equals 和相等运算符的详细信息，请参阅 [Equals 和相等运算符 (==) 的实现准则](/dotnet/standard/design-guidelines/equality-operators)。

## <a name="how-to-investigate-a-warning"></a>如何调查警告
 有关实现 Equals 和相等运算符的示例，请参阅代码分析规则 [CA1815：替代值类型上的 Equals 和相等运算符](../code-quality/ca1815.md)