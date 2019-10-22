---
title: CA1010：集合应实现泛型接口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1010
- CollectionsShouldImplementGenericInterface
helpviewer_keywords:
- CA1010
- CollectionsShouldImplementGenericInterface
ms.assetid: c7d7126f-fa70-40be-8f93-3243e1760dc5
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 20238a844b45221207ca952d90d172ac720136ee
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655252"
---
# <a name="ca1010-collections-should-implement-generic-interface"></a>CA1010：集合应实现泛型接口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|CollectionsShouldImplementGenericInterface|
|CheckId|CA1010|
|类别|Microsoft. Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 外部可见类型实现 <xref:System.Collections.IEnumerable?displayProperty=fullName> 接口，但不实现 <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> 接口，并且包含程序集以 [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] 为目标。 此规则将忽略实现 <xref:System.Collections.IDictionary?displayProperty=fullName> 的类型。

## <a name="rule-description"></a>规则说明
 若要扩大集合的用途，应实现某个泛型集合接口。 然后，该集合可用于填充泛型集合类型，如下所示：

- <xref:System.Collections.Generic.List%601?displayProperty=fullName>

- <xref:System.Collections.Generic.Queue%601?displayProperty=fullName>

- <xref:System.Collections.Generic.Stack%601?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请实现以下泛型集合接口之一：

- <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName>

- <xref:System.Collections.Generic.ICollection%601?displayProperty=fullName>

- <xref:System.Collections.Generic.IList%601?displayProperty=fullName>

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 可以安全地禁止显示此规则发出的警告;但是，此集合的使用限制更多。

## <a name="example-violation"></a>示例冲突

### <a name="description"></a>描述
 下面的示例演示一个派生自非泛型 `CollectionBase` 类的类（引用类型），该类与此规则冲突。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Design.CollectionsGenericViolation#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CollectionsGenericViolation/cs/FxCop.Design.CollectionsGenericViolation.cs#1)]

### <a name="comments"></a>注释
 若要修复与此冲突的冲突，应实现泛型接口，或将基类更改为已实现泛型和非泛型接口（如 `Collection<T>` 类）的类型。

## <a name="fix-by-base-class-change"></a>通过基类更改进行修复

### <a name="description"></a>描述
 下面的示例通过将集合的基类从非泛型 `CollectionBase` 类更改为泛型 `Collection<T>` （[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 中的 `Collection(Of T)`）来修复冲突。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Design.CollectionsGenericBase#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CollectionsGenericBase/cs/FxCop.Design.CollectionsGenericBase.cs#1)]

### <a name="comments"></a>注释
 更改已发布类的基类被视为对现有使用者的重大更改。

## <a name="fix-by-interface-implementation"></a>通过接口实现进行修复

### <a name="description"></a>描述
 下面的示例通过实现以下泛型接口来修复冲突： `IEnumerable<T>`、`ICollection<T>` 和 `IList<T>` （`IEnumerable(Of T)`、`ICollection(Of T)` 和 `IList(Of T)` 中的 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]）。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Design.CollectionsGenericInterface#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CollectionsGenericInterface/cs/FxCop.Design.CollectionsGenericInterface.cs#1)]

## <a name="related-rules"></a>相关规则
 [CA1005：避免泛型类型的参数过多](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1000：不要在泛型类型中声明静态成员](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1002：不要公开泛型列表](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006：不要将泛型类型嵌套在成员签名中](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004：泛型方法应提供类型形参](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1003：使用泛型事件处理程序实例](../code-quality/ca1003-use-generic-event-handler-instances.md)

 [CA1007：在适用处使用泛型](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>请参阅
 [泛型](https://msdn.microsoft.com/library/75ea8509-a4ea-4e7a-a2b3-cf72482e9282)
