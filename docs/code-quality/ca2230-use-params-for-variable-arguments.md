---
title: CA2230:对可变数量的参数使用 params
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- UseParamsForVariableArguments
- CA2230
helpviewer_keywords:
- CA2230
- UseParamsForVariableArguments
ms.assetid: bf98b733-4855-4110-9f16-eba5a9e79421
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0639d30771b3a6bb288ddbf9644dda2efcd5f90d
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231360"
---
# <a name="ca2230-use-params-for-variable-arguments"></a>CA2230:对可变数量的参数使用 params

|||
|-|-|
|TypeName|UseParamsForVariableArguments|
|CheckId|CA2230|
|类别|Microsoft.Usage|
|重大更改|重大|

## <a name="cause"></a>原因
公共或受保护类型包含使用`VarArgs`调用约定的公共或受保护方法。

## <a name="rule-description"></a>规则说明
`VarArgs`调用约定用于采用可变数量的参数的某些方法定义。 使用`VarArgs`调用约定的方法不符合公共语言规范（CLS），并且可能无法跨编程语言访问。

在C#中， `VarArgs`在方法的参数`__arglist`列表以关键字结尾时使用调用约定。 Visual Basic 不支持`VarArgs`调用约定，并且视觉对象C++只允许在使用椭圆`...`表示法的非托管代码中使用。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复中C#此规则的冲突，请使用[params](/dotnet/csharp/language-reference/keywords/params) `__arglist`关键字而不是。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示了两种方法，一个是违反规则的方法，另一个是满足规则的方法。

[!code-csharp[FxCop.Usage.UseParams#1](../code-quality/codesnippet/CSharp/ca2230-use-params-for-variable-arguments_1.cs)]

## <a name="see-also"></a>请参阅

- <xref:System.Reflection.CallingConventions?displayProperty=fullName>
- [语言独立性和与语言无关的组件](/dotnet/standard/language-independence-and-language-independent-components)