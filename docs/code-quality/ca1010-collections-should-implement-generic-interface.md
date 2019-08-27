---
title: CA1010:集合应实现泛型接口
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1010
- CollectionsShouldImplementGenericInterface
helpviewer_keywords:
- CA1010
- CollectionsShouldImplementGenericInterface
ms.assetid: c7d7126f-fa70-40be-8f93-3243e1760dc5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 70a418b211cd4340dba9c15f0bf52e3cdfdf8e8f
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69547912"
---
# <a name="ca1010-collections-should-implement-generic-interface"></a>CA1010:集合应实现泛型接口

|||
|-|-|
|TypeName|CollectionsShouldImplementGenericInterface|
|CheckId|CA1010|
|类别|Microsoft.Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因

类型实现<xref:System.Collections.IEnumerable?displayProperty=fullName>接口, 但不<xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName>实现接口, 而包含程序集面向 .net。 此规则将忽略实现<xref:System.Collections.IDictionary?displayProperty=fullName>的类型。

默认情况下, 此规则仅查看外部可见类型, 但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

若要扩大集合的用途，应实现某个泛型集合接口。 然后, 该集合可用于填充泛型集合类型, 如下所示:

- <xref:System.Collections.Generic.List%601?displayProperty=fullName>
- <xref:System.Collections.Generic.Queue%601?displayProperty=fullName>
- <xref:System.Collections.Generic.Stack%601?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突, 请实现以下泛型集合接口之一:

- <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName>
- <xref:System.Collections.Generic.ICollection%601?displayProperty=fullName>
- <xref:System.Collections.Generic.IList%601?displayProperty=fullName>

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

可以安全地禁止显示此规则发出的警告;但是, 集合的使用会受到更多的限制。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)(而不是传统分析) 运行此规则, 则可以根据其可访问性, 将基本代码的哪些部分配置为在上运行此规则。 例如, 若要指定规则只应针对非公共 API 图面运行, 请在项目中的 editorconfig 文件中添加以下键/值对:

```ini
dotnet_code_quality.ca1010.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则 (设计) 配置此选项。 有关详细信息, 请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="example-violation"></a>示例冲突

下面的示例演示一个派生自非泛型`CollectionBase`类的类 (引用类型), 该类与此规则冲突。

[!code-csharp[FxCop.Design.CollectionsGenericViolation#1](../code-quality/codesnippet/CSharp/ca1010-collections-should-implement-generic-interface_1.cs)]

若要修复与此规则的冲突, 请执行以下操作之一:

- 实现泛型接口。
- 将基类更改为已实现泛型和非泛型接口 (如`Collection<T>`类) 的类型。

## <a name="fix-by-base-class-change"></a>通过基类更改进行修复

下面的示例通过将集合的基类从非泛型`CollectionBase`类更改为泛型`Collection<T>` (`Collection(Of T)`在 Visual Basic 中) 类来修复冲突。

[!code-csharp[FxCop.Design.CollectionsGenericBase#1](../code-quality/codesnippet/CSharp/ca1010-collections-should-implement-generic-interface_2.cs)]

更改已发布类的基类被视为对现有使用者的重大更改。

## <a name="fix-by-interface-implementation"></a>通过接口实现进行修复

下面的示例通过实现以下泛型接口来修复冲突: `IEnumerable<T>`、 `ICollection<T>` `IList(Of T)`和`IList<T>` (`IEnumerable(Of T)`Visual Basic、 `ICollection(Of T)`和)。

[!code-csharp[FxCop.Design.CollectionsGenericInterface#1](../code-quality/codesnippet/CSharp/ca1010-collections-should-implement-generic-interface_3.cs)]

## <a name="related-rules"></a>相关规则

- [CA1005避免泛型类型的参数过多](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)
- [CA1000不要在泛型类型中声明静态成员](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)
- [CA1002不要公开泛型列表](../code-quality/ca1002-do-not-expose-generic-lists.md)
- [CA1006不要将泛型类型嵌套在成员签名中](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)
- [CA1004泛型方法应提供类型参数](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)
- [CA1003使用泛型事件处理程序实例](../code-quality/ca1003-use-generic-event-handler-instances.md)
- [CA1007在适当的位置使用泛型](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>请参阅

- [泛型](/dotnet/csharp/programming-guide/generics/index)