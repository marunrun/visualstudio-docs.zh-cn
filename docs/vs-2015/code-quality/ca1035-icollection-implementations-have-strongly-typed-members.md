---
title: CA1035:ICollection 实现含有强类型成员 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ICollectionImplementationsHaveStronglyTypedMembers
- CA1035
helpviewer_keywords:
- CA1035
- ICollectionImplementationsHaveStronglyTypedMembers
ms.assetid: ad404eb5-cf6a-44b7-b78a-8ebfb654bc7f
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 6eda1bc311c39d0ec1da9667ac078c22183e2bd0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62535744"
---
# <a name="ca1035-icollection-implementations-have-strongly-typed-members"></a>CA1035:ICollection 实现含有强类型成员
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ICollectionImplementationsHaveStronglyTypedMembers|
|CheckId|CA1035|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护类型实现<xref:System.Collections.ICollection?displayProperty=fullName>，但不提供有关强类型化的方法<xref:System.Collections.ICollection.CopyTo%2A?displayProperty=fullName>。 强类型化的版本<xref:System.Collections.ICollection.CopyTo%2A>必须接受两个参数且不能<xref:System.Array?displayProperty=fullName>或一组<xref:System.Object?displayProperty=fullName>作为其第一个参数。

## <a name="rule-description"></a>规则说明
 此规则要求<xref:System.Collections.ICollection>实现提供强类型化成员，因此用户不需要强制转换的自变量<xref:System.Object>键入时它们使用由接口提供的功能。 此规则假定，该类型的实现<xref:System.Collections.ICollection>执行，因此，若要管理的强于类型的实例集合<xref:System.Object>。

 <xref:System.Collections.ICollection> 实现 <xref:System.Collections.IEnumerable?displayProperty=fullName> 接口。 如果集合中的对象扩展<xref:System.ValueType?displayProperty=fullName>，则必须提供的强类型化的成员<xref:System.Collections.IEnumerable.GetEnumerator%2A>以避免由装箱造成的性能下降。 这不需要的对象的集合属于引用类型时。

 若要实现接口成员的强类型化的版本，实现接口成员显式使用窗体名称`InterfaceName.InterfaceMemberName`，如<xref:System.Collections.ICollection.CopyTo%2A>。 显式接口成员由接口中使用的数据类型的声明。 通过使用接口成员名称，如实现强类型的成员<xref:System.Collections.ICollection.CopyTo%2A>。 声明为公共的强类型化的成员和声明参数和返回值是由集合的强类型。 强类型替换较弱的类型，如<xref:System.Object>和<xref:System.Array>，通过接口进行声明。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，请显式实现接口成员 (其声明为<xref:System.Collections.ICollection.CopyTo%2A>)。 添加的强类型化的公共成员，声明为`CopyTo`，并将其采用强类型化的数组作为其第一个参数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果实现基于对象的一个新集合，如二进制树中，扩展新集合的类型确定的强类型，禁止显示此规则的警告。 这些类型应符合此规则，并将强类型化的成员公开。

## <a name="example"></a>示例
 下面的示例演示如何实现的正确方法<xref:System.Collections.ICollection>。

 [!code-csharp[FxCop.Design.ICollectionStrongTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ICollectionStrongTypes/cs/FxCop.Design.ICollectionStrongTypes.cs#1)]

## <a name="related-rules"></a>相关的规则
 [CA1038:枚举数应强类型化](../code-quality/ca1038-enumerators-should-be-strongly-typed.md)

 [CA1039:列表已强类型化](../code-quality/ca1039-lists-are-strongly-typed.md)

## <a name="see-also"></a>请参阅
 <xref:System.Array?displayProperty=fullName> <xref:System.Collections.IEnumerable?displayProperty=fullName>
 <xref:System.Collections.ICollection?displayProperty=fullName>
 <xref:System.Object?displayProperty=fullName>
