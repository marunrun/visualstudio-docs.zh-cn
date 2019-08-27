---
title: CA1038:枚举数应强类型化
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EnumeratorsShouldBeStronglyTyped
- CA1038
helpviewer_keywords:
- EnumeratorsShouldBeStronglyTyped
- CA1038
ms.assetid: 8919f526-d487-42a4-87dc-2b2ee25260c4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2dae77bf7783edc165305f9b3ba60969d4f126a8
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922891"
---
# <a name="ca1038-enumerators-should-be-strongly-typed"></a>CA1038:枚举数应强类型化

|||
|-|-|
|TypeName|EnumeratorsShouldBeStronglyTyped|
|CheckId|CA1038|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
公共或受保护类型实现<xref:System.Collections.IEnumerator?displayProperty=fullName> , <xref:System.Collections.IEnumerator.Current%2A?displayProperty=fullName>但不提供属性的强类型版本。 从以下类型派生的类型将从此规则中免除:

- <xref:System.Collections.CollectionBase?displayProperty=fullName>

- <xref:System.Collections.DictionaryBase?displayProperty=fullName>

- <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>

## <a name="rule-description"></a>规则说明
此规则要求<xref:System.Collections.IEnumerator>实现还需要提供<xref:System.Collections.IEnumerator.Current%2A>属性的强类型版本, 以便用户在使用该接口提供的功能时无需将返回值强制转换为强类型。 此规则假定实现<xref:System.Collections.IEnumerator>的类型包含强于<xref:System.Object>的类型的实例集合。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请显式实现接口属性 (将其`IEnumerator.Current`声明为)。 添加属性的公共强类型版本, 将声明为`Current`, 并使其返回强类型化对象。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
当您实现基于对象的枚举器以便与基于对象的集合 (如二元树) 一起使用时, 禁止显示此规则发出的警告。 扩展新集合的类型将定义强类型枚举器并公开强类型的属性。

## <a name="example"></a>示例
下面的示例演示实现强类型<xref:System.Collections.IEnumerator>类型的正确方法。

[!code-csharp[FxCop.Design.IEnumeratorStrongTypes#1](../code-quality/codesnippet/CSharp/ca1038-enumerators-should-be-strongly-typed_1.cs)]

## <a name="related-rules"></a>相关规则
[CA1035ICollection 实现具有强类型成员](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md)

[CA1039列表已强类型化](../code-quality/ca1039-lists-are-strongly-typed.md)

## <a name="see-also"></a>请参阅

- <xref:System.Collections.IEnumerator?displayProperty=fullName>
- <xref:System.Collections.CollectionBase?displayProperty=fullName>
- <xref:System.Collections.DictionaryBase?displayProperty=fullName>
- <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>