---
title: CA1025:用形参数组替换重复的实参
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1025
- ReplaceRepetitiveArgumentsWithParamsArray
helpviewer_keywords:
- ReplaceRepetitiveArgumentsWithParamsArray
- CA1025
ms.assetid: f009b340-dea3-4459-8fe1-2143aa8b5d0b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f65d64dd4e881c41b17cd7cb9dc072a6fe800766
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236136"
---
# <a name="ca1025-replace-repetitive-arguments-with-params-array"></a>CA1025:用形参数组替换重复的实参

|||
|-|-|
|TypeName|ReplaceRepetitiveArgumentsWithParamsArray|
|CheckId|CA1025|
|类别|Microsoft.Design|
|重大更改|不间断|

## <a name="cause"></a>原因
公共类型中的公共或受保护方法包含三个以上的参数，其最后三个参数的类型相同。

## <a name="rule-description"></a>规则说明
如果参数的精确数量未知且变量参数为同一类型，或者可以作为相同的类型传递，请使用参数数组而不是重复的参数。 例如， <xref:System.Console.WriteLine%2A>方法提供了一个常规用途重载，该重载使用参数数组接受任意数量的<xref:System.Object>自变量。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请将重复参数替换为参数数组。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
禁止显示此规则发出的警告始终是安全的;但是，这种设计可能会导致可用性问题。

## <a name="example"></a>示例
下面的示例演示违反此规则的类型。

[!code-csharp[FxCop.Design.RepeatArgs#1](../code-quality/codesnippet/CSharp/ca1025-replace-repetitive-arguments-with-params-array_1.cs)]