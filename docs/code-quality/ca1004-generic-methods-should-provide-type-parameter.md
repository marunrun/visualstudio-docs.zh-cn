---
title: CA1004:泛型方法应提供类型参数
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1004
- GenericMethodsShouldProvideTypeParameter
helpviewer_keywords:
- GenericMethodsShouldProvideTypeParameter
- CA1004
ms.assetid: 38755f6a-fb45-4bf2-932e-0354ad826499
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 9a09d06a521c4751e3aea78b72b99a8126f4e7ff
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923250"
---
# <a name="ca1004-generic-methods-should-provide-type-parameter"></a>CA1004:泛型方法应提供类型参数

|||
|-|-|
|TypeName|GenericMethodsShouldProvideTypeParameter|
|CheckId|CA1004|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
外部可见泛型方法的参数签名不包含对应于该方法的所有类型参数的类型。

## <a name="rule-description"></a>规则说明
推理是指由传递给泛型方法的自变量类型来确定该方法的类型参数，而不是显式指定类型参数。 若要启用推理，泛型方法的参数签名必须包含与该方法的类型参数属于相同类型的参数。 在这种情况下，不必指定类型参数。 如果对所有类型参数使用推理, 则调用泛型和非泛型实例方法的语法是相同的。 这简化了泛型方法的可用性。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请更改设计, 使参数签名对于该方法的每个类型参数都包含相同的类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。 在易于理解和使用的语法中提供泛型, 可减少学习和增加新库的采用率所需的时间。

## <a name="example"></a>示例
下面的示例演示了调用两种泛型方法的语法。 推断的类型参数`InferredTypeArgument` , `NotInferredTypeArgument`必须显式指定的类型自变量。

[!code-vb[FxCop.Design.Inference#1](../code-quality/codesnippet/VisualBasic/ca1004-generic-methods-should-provide-type-parameter_1.vb)]
[!code-csharp[FxCop.Design.Inference#1](../code-quality/codesnippet/CSharp/ca1004-generic-methods-should-provide-type-parameter_1.cs)]

## <a name="related-rules"></a>相关规则
[CA1005避免泛型类型的参数过多](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

[CA1010集合应实现泛型接口](../code-quality/ca1010-collections-should-implement-generic-interface.md)

[CA1000不要在泛型类型中声明静态成员](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

[CA1002不要公开泛型列表](../code-quality/ca1002-do-not-expose-generic-lists.md)

[CA1006不要将泛型类型嵌套在成员签名中](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

[CA1003使用泛型事件处理程序实例](../code-quality/ca1003-use-generic-event-handler-instances.md)

[CA1007在适当的位置使用泛型](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>请参阅
[泛型](/dotnet/csharp/programming-guide/generics/index)