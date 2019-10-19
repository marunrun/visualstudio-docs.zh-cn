---
title: CA1007：在适当的位置使用泛型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1007
- UseGenericsWhereAppropriate
helpviewer_keywords:
- CA1007
- UseGenericsWhereAppropriate
ms.assetid: eab780ea-3b1f-4d32-b15a-5d48da2df46b
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 22c9bac17a957438ee8d2a6f4b634f30604ed1ff
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668958"
---
# <a name="ca1007-use-generics-where-appropriate"></a>CA1007：在适用处使用泛型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|UseGenericsWhereAppropriate|
|CheckId|CA1007|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见方法包含类型 <xref:System.Object?displayProperty=fullName> 的引用参数，而包含的程序集目标 [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)]。

## <a name="rule-description"></a>规则说明
 引用参数是使用 `ref` `ByRef` （[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]）关键字修改的参数。 为引用参数提供的参数类型必须与引用参数类型完全匹配。 若要使用从引用参数类型派生的类型，必须先强制转换类型并将其分配给引用参数类型的变量。 如果使用泛型方法，则允许将受约束的所有类型传递给方法，而无需先将类型强制转换为引用参数类型。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将方法设置为泛型，并使用类型参数替换 <xref:System.Object> 参数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示了一种通用的交换例程，该例程作为非泛型方法和泛型方法实现。 请注意，与非泛型方法相比，使用泛型方法交换字符串的效率。

 [!code-csharp[FxCop.Design.UseGenerics#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.UseGenerics/cs/FxCop.Design.UseGenerics.cs#1)]
 [!code-vb[FxCop.Design.UseGenerics#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.UseGenerics/vb/FxCop.Design.UseGenerics.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1005：避免泛型类型的参数过多](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1010：集合应实现泛型接口](../code-quality/ca1010-collections-should-implement-generic-interface.md)

 [CA1000：不要在泛型类型中声明静态成员](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1002：不要公开泛型列表](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006：不要将泛型类型嵌套在成员签名中](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004：泛型方法应提供类型形参](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1003：使用泛型事件处理程序实例](../code-quality/ca1003-use-generic-event-handler-instances.md)

## <a name="see-also"></a>请参阅
 [泛型](https://msdn.microsoft.com/library/75ea8509-a4ea-4e7a-a2b3-cf72482e9282)
