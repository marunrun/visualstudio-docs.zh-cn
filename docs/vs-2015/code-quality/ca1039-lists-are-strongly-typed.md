---
title: CA1039:列表已强类型化 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 3fb1a6255539ded989c5ad9638fc961d606a19f7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62559738"
---
# <a name="ca1039-lists-are-strongly-typed"></a>CA1039:列表已强类型化
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ListsAreStronglyTyped|
|CheckId|CA1039|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护类型实现<xref:System.Collections.IList?displayProperty=fullName>但不提供强类型化的方法的一个或多项操作：

- IList.Item

- IList.Add

- IList.Contains

- IList.IndexOf

- IList.Insert

- IList.Remove

## <a name="rule-description"></a>规则说明
 此规则要求<xref:System.Collections.IList>实现提供强类型化成员，因此用户不需要强制转换的自变量<xref:System.Object?displayProperty=fullName>键入时它们使用由接口提供的功能。 <xref:System.Collections.IList>接口由可按照索引访问的对象的集合实现。 此规则假定，该类型的实现<xref:System.Collections.IList>这样做是为了管理强于类型的实例的集合<xref:System.Object>。

 <xref:System.Collections.IList> 实现<xref:System.Collections.ICollection?displayProperty=fullName>和<xref:System.Collections.IEnumerable?displayProperty=fullName>接口。 如果你实现了<xref:System.Collections.IList>，则必须提供必需的强类型化的成员<xref:System.Collections.ICollection>。 如果集合中的对象扩展<xref:System.ValueType?displayProperty=fullName>，则必须提供的强类型化的成员<xref:System.Collections.IEnumerable.GetEnumerator%2A>以避免性能降低由装箱造成; 这不是必需的对象的集合属于引用类型时。

 若要符合此规则，实现接口成员显式使用名称形式 InterfaceName.InterfaceMemberName，类似于<xref:System.Collections.IList.Add%2A>。 显式接口成员由接口中使用的数据类型的声明。 通过使用接口成员名称，如实现强类型的成员`Add`。 声明为公共的强类型化的成员和声明参数和返回值是由集合的强类型。 强类型替换较弱的类型，如<xref:System.Object>和<xref:System.Array>，通过接口进行声明。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，显式实现<xref:System.Collections.IList>成员，并为前面记下的成员提供强类型替代项。 代码正确地实现<xref:System.Collections.IList>接口，并提供所需强类型的成员，请参阅下面的示例。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 实现基于对象的新集合，如链接列表，其中扩展新集合的类型决定强类型时，禁止显示此规则的警告。 这些类型应符合此规则，并将强类型化的成员公开。

## <a name="example"></a>示例
 在下面的示例中，类型`YourType`扩展了<xref:System.Collections.CollectionBase?displayProperty=fullName>，也应如此所有强类型的集合。 请注意，<xref:System.Collections.CollectionBase>提供的显式实现<xref:System.Collections.IList>接口供你。 因此，您必须仅提供的强类型化的成员<xref:System.Collections.IList>和<xref:System.Collections.ICollection>。

 [!code-csharp[FxCop.Design.IListStrongTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IListStrongTypes/cs/FxCop.Design.IListStrongTypes.cs#1)]

## <a name="related-rules"></a>相关的规则
 [CA1035:ICollection 实现含有强类型成员](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md)

 [CA1038:枚举数应强类型化](../code-quality/ca1038-enumerators-should-be-strongly-typed.md)

## <a name="see-also"></a>请参阅
 <xref:System.Collections.CollectionBase?displayProperty=fullName> <xref:System.Collections.ICollection?displayProperty=fullName>
 <xref:System.Collections.IEnumerable?displayProperty=fullName>
 <xref:System.Collections.IList?displayProperty=fullName>
 <xref:System.Object?displayProperty=fullName>
