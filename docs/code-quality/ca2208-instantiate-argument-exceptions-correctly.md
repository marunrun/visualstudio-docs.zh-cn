---
title: CA2208:正确实例化参数异常
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2208
- InstantiateArgumentExceptionsCorrectly
helpviewer_keywords:
- InstantiateArgumentExceptionsCorrectly
- CA2208
ms.assetid: e2a48939-d9fa-478c-b2f9-3bdbce07dff7
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 2110a8d0b58d87a4554971cf00af6441d293aa91
ms.sourcegitcommit: 92a04c57ac0a49f304fa2ea5043436f30068c3cd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975894"
---
# <a name="ca2208-instantiate-argument-exceptions-correctly"></a>CA2208:正确实例化参数异常

|||
|-|-|
|TypeName|InstantiateArgumentExceptionsCorrectly|
|CheckId|CA2208|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

可能的原因包括以下情况：

- 调用的是，或其派生，异常类型的默认 （无参数） 构造函数<xref:System.ArgumentException>。

- 不正确的字符串参数传递给参数化构造函数的异常类型或其派生， <xref:System.ArgumentException>。

## <a name="rule-description"></a>规则说明

而不是调用默认构造函数，调用允许更有意义的异常消息提供的构造函数重载之一。 异常消息应面向开发人员，并清楚地解释错误条件以及如何更正或避免异常。

一个或两个字符串的构造函数的签名<xref:System.ArgumentException>及其派生的类型而不相对于位置一致`message`和`paramName`参数。 请确保使用正确的字符串参数调用这些构造函数。 签名如下所示：

- <xref:System.ArgumentException>(字符串`message`)
- <xref:System.ArgumentException>(字符串`message`，字符串`paramName`)
- <xref:System.ArgumentNullException>(字符串`paramName`)
- <xref:System.ArgumentNullException>(字符串`paramName`，字符串`message`)
- <xref:System.ArgumentOutOfRangeException>(字符串`paramName`)
- <xref:System.ArgumentOutOfRangeException>(字符串`paramName`，字符串`message`)
- <xref:System.DuplicateWaitObjectException>(字符串`parameterName`)
- <xref:System.DuplicateWaitObjectException>(字符串`parameterName`，字符串`message`)

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请调用的构造函数的一条消息、 参数名称，或两者，并确保参数是正确的类型的<xref:System.ArgumentException>被调用。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

它可以安全地禁止显示此规则的警告，如果使用正确的字符串自变量调用参数化构造函数。

## <a name="example"></a>示例

下面的代码演示正确实例化的实例的构造函数<xref:System.ArgumentNullException>。

[!code-cpp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../code-quality/codesnippet/CPP/ca2208-instantiate-argument-exceptions-correctly_1.cpp)]
[!code-csharp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../code-quality/codesnippet/CSharp/ca2208-instantiate-argument-exceptions-correctly_1.cs?range=3-6)]
[!code-vb[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../code-quality/codesnippet/VisualBasic/ca2208-instantiate-argument-exceptions-correctly_1.vb)]

下面的代码通过切换构造函数参数修复了上一冲突。

[!code-cpp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../code-quality/codesnippet/CPP/ca2208-instantiate-argument-exceptions-correctly_2.cpp)]
[!code-csharp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../code-quality/codesnippet/CSharp/ca2208-instantiate-argument-exceptions-correctly_2.cs?range=3-6)]
[!code-vb[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../code-quality/codesnippet/VisualBasic/ca2208-instantiate-argument-exceptions-correctly_2.vb)]

## <a name="related-rules"></a>相关的规则

- [CA1507:使用 nameof 替代字符串](ca1507.md)