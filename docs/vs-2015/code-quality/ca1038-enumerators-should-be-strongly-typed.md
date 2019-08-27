---
title: CA1038:枚举数应强类型化 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- EnumeratorsShouldBeStronglyTyped
- CA1038
helpviewer_keywords:
- EnumeratorsShouldBeStronglyTyped
- CA1038
ms.assetid: 8919f526-d487-42a4-87dc-2b2ee25260c4
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 84b6ae6ef0c63870ad9dc593fd0cf2e166e65397
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62559808"
---
# <a name="ca1038-enumerators-should-be-strongly-typed"></a>CA1038:枚举数应强类型化
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|EnumeratorsShouldBeStronglyTyped|
|CheckId|CA1038|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护类型实现<xref:System.Collections.IEnumerator?displayProperty=fullName>，但不提供强类型的版本<xref:System.Collections.IEnumerator.Current%2A?displayProperty=fullName>属性。 从以下类型派生的类型不受此规则：

- <xref:System.Collections.CollectionBase?displayProperty=fullName>

- <xref:System.Collections.DictionaryBase?displayProperty=fullName>

- <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>

## <a name="rule-description"></a>规则说明
 此规则要求<xref:System.Collections.IEnumerator>实现还提供强类型的版本<xref:System.Collections.IEnumerator.Current%2A>属性，因此用户不需要返回值转换为强类型使用时，它们提供的功能由接口。 此规则假定，该类型的实现<xref:System.Collections.IEnumerator>包含一系列强于类型的实例<xref:System.Object>。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，请显式实现接口属性 (其声明为`IEnumerator.Current`)。 添加的属性，声明为公共的强类型化的版本`Current`，并使其返回强类型化的对象。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 实现基于对象的枚举数，以使用与基于对象的集合，如二进制树时，禁止显示此规则的警告。 扩展的新集合的类型将定义强类型化枚举器，并公开强类型化的属性。

## <a name="example"></a>示例
 下面的示例演示如何实现强类型化的正确方法<xref:System.Collections.IEnumerator>类型。

 [!code-csharp[FxCop.Design.IEnumeratorStrongTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IEnumeratorStrongTypes/cs/FxCop.Design.IEnumeratorStrongTypes.cs#1)]

## <a name="related-rules"></a>相关的规则
 [CA1035:ICollection 实现含有强类型成员](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md)

 [CA1039:列表已强类型化](../code-quality/ca1039-lists-are-strongly-typed.md)

## <a name="see-also"></a>请参阅
 <xref:System.Collections.IEnumerator?displayProperty=fullName> <xref:System.Collections.CollectionBase?displayProperty=fullName>
 <xref:System.Collections.DictionaryBase?displayProperty=fullName>
 <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>
