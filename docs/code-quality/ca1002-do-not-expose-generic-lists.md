---
title: CA1002:不要公开泛型列表
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DoNotExposeGenericLists
- CA1002
helpviewer_keywords:
- CA1002
- DoNotExposeGenericLists
ms.assetid: 5caac810-1a79-47df-a27b-c46c5040bf34
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a6e300edf07aa98facbe6059ba9574e238ec8f3e
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923259"
---
# <a name="ca1002-do-not-expose-generic-lists"></a>CA1002:不要公开泛型列表

|||
|-|-|
|TypeName|DoNotExposeGenericLists|
|CheckId|CA1002|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
类型包含外部可见的成员, 该成员是<xref:System.Collections.Generic.List%601?displayProperty=fullName>类型、 <xref:System.Collections.Generic.List%601?displayProperty=fullName>返回类型<xref:System.Collections.Generic.List%601?displayProperty=fullName>或其签名包含参数。

## <a name="rule-description"></a>规则说明
 <xref:System.Collections.Generic.List%601?displayProperty=fullName>是为性能而不是继承而设计的泛型集合。 <xref:System.Collections.Generic.List%601?displayProperty=fullName>不包含使更改继承类的行为变得更简单的虚拟成员。 以下泛型集合是为继承设计的, 应公开, 而不<xref:System.Collections.Generic.List%601?displayProperty=fullName>是公开。

- <xref:System.Collections.ObjectModel.Collection%601?displayProperty=fullName>

- <xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=fullName>

- <xref:System.Collections.ObjectModel.KeyedCollection%602?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请<xref:System.Collections.Generic.List%601?displayProperty=fullName>将类型更改为为继承而设计的泛型集合之一。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
请勿禁止显示此规则发出的警告, 除非引发此警告的程序集不是可重用的库。 例如, 可以安全地在性能优化的应用程序中禁止显示此警告, 因为使用的是泛型列表。

## <a name="related-rules"></a>相关规则
[CA1005避免泛型类型的参数过多](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

[CA1010集合应实现泛型接口](../code-quality/ca1010-collections-should-implement-generic-interface.md)

[CA1000不要在泛型类型中声明静态成员](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

[CA1006不要将泛型类型嵌套在成员签名中](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

[CA1004泛型方法应提供类型参数](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

[CA1003使用泛型事件处理程序实例](../code-quality/ca1003-use-generic-event-handler-instances.md)

[CA1007在适当的位置使用泛型](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>请参阅
[泛型](/dotnet/csharp/programming-guide/generics/index)