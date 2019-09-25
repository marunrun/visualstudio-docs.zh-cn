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
ms.openlocfilehash: 9f9425ab1ea9eadd3bd06d950118ce83ba5c35f9
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231647"
---
# <a name="ca2208-instantiate-argument-exceptions-correctly"></a>CA2208:正确实例化参数异常

|||
|-|-|
|TypeName|InstantiateArgumentExceptionsCorrectly|
|CheckId|CA2208|
|类别|Microsoft.Usage|
|重大更改|不间断|

## <a name="cause"></a>原因

可能的原因包括以下情况：

- 调用了异常类型的默认（无参数）构造函数，或派生自<xref:System.ArgumentException>。

- 将不正确的字符串自变量传递给异常类型的参数化构造函数，或派生自<xref:System.ArgumentException>。

## <a name="rule-description"></a>规则说明

不是调用默认构造函数，而是调用允许提供更有意义的异常消息的构造函数重载之一。 异常消息应面向开发人员，并清楚地说明错误情况以及如何纠正或避免异常。

<xref:System.ArgumentException>及其派生类型的一个和两个字符串构造函数的签名与位置`message`和`paramName`参数不一致。 请确保用正确的字符串参数调用这些构造函数。 签名如下所示：

- <xref:System.ArgumentException>（string `message`）
- <xref:System.ArgumentException>（string `message`，string `paramName`）
- <xref:System.ArgumentNullException>（string `paramName`）
- <xref:System.ArgumentNullException>（string `paramName`，string `message`）
- <xref:System.ArgumentOutOfRangeException>（string `paramName`）
- <xref:System.ArgumentOutOfRangeException>（string `paramName`，string `message`）
- <xref:System.DuplicateWaitObjectException>（string `parameterName`）
- <xref:System.DuplicateWaitObjectException>（string `parameterName`，string `message`）

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请调用使用消息的构造函数和/或参数名，并确保参数对于调用的类型<xref:System.ArgumentException>是正确的。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

仅当使用正确的字符串参数调用参数化的构造函数时，才可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例

下面的代码演示了一个错误地实例化实例的<xref:System.ArgumentNullException>构造函数。

[!code-cpp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../code-quality/codesnippet/CPP/ca2208-instantiate-argument-exceptions-correctly_1.cpp)]
[!code-csharp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../code-quality/codesnippet/CSharp/ca2208-instantiate-argument-exceptions-correctly_1.cs?range=3-6)]
[!code-vb[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../code-quality/codesnippet/VisualBasic/ca2208-instantiate-argument-exceptions-correctly_1.vb)]

下面的代码通过切换构造函数参数来修复前面的冲突。

[!code-cpp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../code-quality/codesnippet/CPP/ca2208-instantiate-argument-exceptions-correctly_2.cpp)]
[!code-csharp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../code-quality/codesnippet/CSharp/ca2208-instantiate-argument-exceptions-correctly_2.cs?range=3-6)]
[!code-vb[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../code-quality/codesnippet/VisualBasic/ca2208-instantiate-argument-exceptions-correctly_2.vb)]

## <a name="related-rules"></a>相关规则

- [CA1507:使用 nameof 代替字符串](ca1507.md)