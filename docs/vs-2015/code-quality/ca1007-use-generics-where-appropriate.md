---
title: CA1007:在适用处使用泛型 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 2d4f5f7749ad34f62e9dfa5718c6a778d6e7bebf
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704296"
---
# <a name="ca1007-use-generics-where-appropriate"></a>CA1007:在适用处使用泛型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|UseGenericsWhereAppropriate|
|CheckId|CA1007|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见方法包含类型的引用参数<xref:System.Object?displayProperty=fullName>，并包含程序集针对[!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)]。

## <a name="rule-description"></a>规则说明
 引用参数是一个参数，通过修改`ref`(`ByRef`中[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) 关键字。 为引用参数提供的自变量类型必须与引用参数类型完全匹配。 若要使用派生自引用参数类型的类型，该类型必须首先进行强制转换和分配给引用参数类型的变量。 使用泛型方法，所有类型，受约束，以传递给该方法，而无需第一个强制转换为引用参数类型的类型。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，使该方法成为泛型函数和替换<xref:System.Object>通过使用类型参数的参数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示实现为非泛型和泛型方法的常规用途的交换例程。 请注意如何有效地使用与非泛型方法的泛型方法交换字符串。

 [!code-csharp[FxCop.Design.UseGenerics#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.UseGenerics/cs/FxCop.Design.UseGenerics.cs#1)]
 [!code-vb[FxCop.Design.UseGenerics#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.UseGenerics/vb/FxCop.Design.UseGenerics.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA1005:避免泛型类型参数过多](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1010:集合应实现泛型接口](../code-quality/ca1010-collections-should-implement-generic-interface.md)

 [CA1000:不要在泛型类型中声明静态成员](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1002:不要公开泛型列表](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006:不要将嵌套在成员签名中的泛型类型](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004:泛型方法应提供类型参数](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1003:使用泛型事件处理程序实例](../code-quality/ca1003-use-generic-event-handler-instances.md)

## <a name="see-also"></a>请参阅
 [泛型](https://msdn.microsoft.com/library/75ea8509-a4ea-4e7a-a2b3-cf72482e9282)
