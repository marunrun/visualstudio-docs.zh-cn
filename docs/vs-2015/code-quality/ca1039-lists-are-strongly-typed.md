---
title: CA1039： Lists 为强类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1039
- ListsAreStronglyTyped
helpviewer_keywords:
- CA1039
- ListsAreStronglyTyped
ms.assetid: 5ac366c4-fd87-4d5c-95d5-f755510c8e5c
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 4e485375c12564b5416c79bd3a41dedb1da76dc0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533440"
---
# <a name="ca1039-lists-are-strongly-typed"></a>CA1039:列表已强类型化
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|ListsAreStronglyTyped|
|CheckId|CA1039|
|Category|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护类型实现 <xref:System.Collections.IList?displayProperty=fullName> ，但不为以下一项或多项提供强类型方法：

- IList 项

- IList。添加

- IList。 Contains

- IList. IndexOf

- IList。 Insert

- IList。删除

## <a name="rule-description"></a>规则描述
 此规则要求 <xref:System.Collections.IList> 实现提供强类型成员，使用户在使用该接口提供的功能时无需将参数转换为 <xref:System.Object?displayProperty=fullName> 类型。 <xref:System.Collections.IList>接口由可通过索引访问的对象集合实现。 此规则假定实现的类型 <xref:System.Collections.IList> 执行此来管理强于的类型的实例集合 <xref:System.Object> 。

 <xref:System.Collections.IList>实现 <xref:System.Collections.ICollection?displayProperty=fullName> 和 <xref:System.Collections.IEnumerable?displayProperty=fullName> 接口。 如果实现 <xref:System.Collections.IList> ，则必须为提供必需的强类型成员 <xref:System.Collections.ICollection> 。 如果集合中的对象已扩展 <xref:System.ValueType?displayProperty=fullName> ，则必须为提供强类型成员， <xref:System.Collections.IEnumerable.GetEnumerator%2A> 以避免由装箱导致的性能降低; 当集合的对象为引用类型时，这不是必需的。

 若要遵守此规则，请使用 InterfaceName. InterfaceMemberName 格式的名称显式实现接口成员，例如 <xref:System.Collections.IList.Add%2A> 。 显式接口成员使用接口声明的数据类型。 使用接口成员名称（如）实现强类型成员 `Add` 。 将强类型成员声明为公共成员，并将参数和返回值声明为集合管理的强类型。 强类型取代 <xref:System.Object> 了接口所声明的更弱类型，如和 <xref:System.Array> 。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请显式实现 <xref:System.Collections.IList> 成员并为之前提到的成员提供强类型化替代项。 对于正确实现 <xref:System.Collections.IList> 接口并提供所需强类型成员的代码，请参阅以下示例。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 当您实现新的基于对象的集合（如链接列表，扩展新集合的类型确定强类型）时，禁止显示此规则发出的警告。 这些类型应符合此规则并公开强类型成员。

## <a name="example"></a>示例
 在下面的示例中，类型 `YourType` 扩展了 <xref:System.Collections.CollectionBase?displayProperty=fullName> ，就像所有强类型化集合一样。 请注意， <xref:System.Collections.CollectionBase> 为你提供接口的显式实现 <xref:System.Collections.IList> 。 因此，你必须仅为和提供强类型成员 <xref:System.Collections.IList> <xref:System.Collections.ICollection> 。

 [!code-csharp[FxCop.Design.IListStrongTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IListStrongTypes/cs/FxCop.Design.IListStrongTypes.cs#1)]

## <a name="related-rules"></a>相关规则
 [CA1035:ICollection 实现含有强类型成员](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md)

 [CA1038:枚举数应强类型化](../code-quality/ca1038-enumerators-should-be-strongly-typed.md)

## <a name="see-also"></a>另请参阅
 <xref:System.Collections.CollectionBase?displayProperty=fullName> <xref:System.Collections.ICollection?displayProperty=fullName>
 <xref:System.Collections.IEnumerable?displayProperty=fullName>
 <xref:System.Collections.IList?displayProperty=fullName>
 <xref:System.Object?displayProperty=fullName>
