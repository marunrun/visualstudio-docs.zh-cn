---
title: CA1004:泛型方法应提供类型参数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1004
- GenericMethodsShouldProvideTypeParameter
helpviewer_keywords:
- GenericMethodsShouldProvideTypeParameter
- CA1004
ms.assetid: 38755f6a-fb45-4bf2-932e-0354ad826499
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 458817ee19269735be181e08ed12ee1ecdee329f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68182624"
---
# <a name="ca1004-generic-methods-should-provide-type-parameter"></a>CA1004:泛型方法应提供类型参数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|GenericMethodsShouldProvideTypeParameter|
|CheckId|CA1004|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见的泛型方法的参数签名不包含对应于方法的所有类型参数的类型。

## <a name="rule-description"></a>规则说明
 推理是指由传递给泛型方法的自变量类型来确定该方法的类型参数，而不是显式指定类型参数。 若要启用推理，泛型方法的参数签名必须包含与该方法的类型参数属于相同类型的参数。 在这种情况下，不必指定类型参数。 对所有类型参数使用推理，调用泛型和非泛型实例方法的语法是完全相同。 这简化了泛型方法的可用性。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，更改设计以使参数签名包含方法的每个类型参数的同一类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 提供易于理解和使用的语法中的泛型可减少所需了解和提高新库的使用率的时间。

## <a name="example"></a>示例
 下面的示例显示了调用两个泛型方法的语法。 类型参数`InferredTypeArgument`推断，和的类型参数`NotInferredTypeArgument`必须显式指定。

 [!code-csharp[FxCop.Design.Inference#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.Inference/cs/FxCop.Design.Inference.cs#1)]
 [!code-vb[FxCop.Design.Inference#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.Inference/vb/FxCop.Design.Inference.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA1005:避免泛型类型参数过多](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1010:集合应实现泛型接口](../code-quality/ca1010-collections-should-implement-generic-interface.md)

 [CA1000:不要在泛型类型中声明静态成员](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1002:不要公开泛型列表](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006:不要将嵌套在成员签名中的泛型类型](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1003:使用泛型事件处理程序实例](../code-quality/ca1003-use-generic-event-handler-instances.md)

 [CA1007： 在适用处在适用处使用泛型](../code-quality/ca1007-use-generics-where-appropriate.md)