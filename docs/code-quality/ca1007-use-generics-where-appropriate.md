---
title: CA1007:在适用处使用泛型
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1007
- UseGenericsWhereAppropriate
helpviewer_keywords:
- CA1007
- UseGenericsWhereAppropriate
ms.assetid: eab780ea-3b1f-4d32-b15a-5d48da2df46b
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: ffb18316b5f009a0f2854c8a158e528f15c92326
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923210"
---
# <a name="ca1007-use-generics-where-appropriate"></a>CA1007:在适用处使用泛型

|||
|-|-|
|TypeName|UseGenericsWhereAppropriate|
|CheckId|CA1007|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
外部可见的方法包含类型<xref:System.Object?displayProperty=fullName>的引用参数, 而包含的程序集目标 .NET Framework 2.0。

## <a name="rule-description"></a>规则说明
引用参数是使用`ref` (`ByRef` in [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) 关键字修改的参数。 为引用参数提供的参数类型必须与引用参数类型完全匹配。 若要使用从引用参数类型派生的类型, 必须先强制转换类型并将其分配给引用参数类型的变量。 如果使用泛型方法, 则允许将受约束的所有类型传递给方法, 而无需先将类型强制转换为引用参数类型。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请将方法设置为泛型<xref:System.Object> , 并使用类型参数替换参数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示了一种通用的交换例程, 该例程作为非泛型方法和泛型方法实现。 请注意, 与非泛型方法相比, 使用泛型方法交换字符串的效率。

[!code-vb[FxCop.Design.UseGenerics#1](../code-quality/codesnippet/VisualBasic/ca1007-use-generics-where-appropriate_1.vb)]
[!code-csharp[FxCop.Design.UseGenerics#1](../code-quality/codesnippet/CSharp/ca1007-use-generics-where-appropriate_1.cs)]

## <a name="related-rules"></a>相关规则
[CA1005避免泛型类型的参数过多](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

[CA1010集合应实现泛型接口](../code-quality/ca1010-collections-should-implement-generic-interface.md)

[CA1000不要在泛型类型中声明静态成员](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

[CA1002不要公开泛型列表](../code-quality/ca1002-do-not-expose-generic-lists.md)

[CA1006不要将泛型类型嵌套在成员签名中](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

[CA1004泛型方法应提供类型参数](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

[CA1003使用泛型事件处理程序实例](../code-quality/ca1003-use-generic-event-handler-instances.md)

## <a name="see-also"></a>请参阅
[泛型](/dotnet/csharp/programming-guide/generics/index)