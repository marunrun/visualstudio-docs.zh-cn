---
title: CA2227：集合属性应为只读 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2227
- CollectionPropertiesShouldBeReadOnly
helpviewer_keywords:
- CA2227
- CollectionPropertiesShouldBeReadOnly
ms.assetid: 26967aaf-6fbe-438a-b4d3-ac579b5dc0f9
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 8aee6f7172414de809d964652411c1f077fe0cdd
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658861"
---
# <a name="ca2227-collection-properties-should-be-read-only"></a>CA2227：集合属性应为只读
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|CollectionPropertiesShouldBeReadOnly|
|CheckId|CA2227|
|类别|Microsoft. 使用情况|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见的可写属性是实现 <xref:System.Collections.ICollection?displayProperty=fullName> 的类型。 规则将忽略数组、索引器（名称为 "Item" 的属性）和权限集。

## <a name="rule-description"></a>规则说明
 可写集合属性允许用户将集合替换为完全不同的集合。 只读属性禁止替换该集合，但仍允许设置单个成员。 如果替换集合是一个目标，则首选的设计模式是包含一个方法，用于从集合中移除所有元素，使用一个方法来重新填充集合。 有关此模式的示例，请参阅 <xref:System.Collections.ArrayList?displayProperty=fullName> 类的 <xref:System.Collections.ArrayList.Clear%2A> 和 <xref:System.Collections.ArrayList.AddRange%2A> 方法。

 二进制和 XML 序列化都支持作为集合的只读属性。 @No__t_0 类对于实现 <xref:System.Collections.ICollection> 和 <xref:System.Collections.IEnumerable?displayProperty=fullName> 以便能够序列化的类型具有特定的要求。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将属性设置为只读，如果设计需要，请添加方法以清除并重新填充集合。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示一个具有可写集合属性的类型，并演示如何直接替换该集合。 此外，还会显示使用 `Clear` 和 `AddRange` 方法替换只读集合属性的首选方式。

 [!code-cpp[FxCop.Usage.PropertiesReturningCollections#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.PropertiesReturningCollections/cpp/FxCop.Usage.PropertiesReturningCollections.cpp#1)]
 [!code-csharp[FxCop.Usage.PropertiesReturningCollections#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.PropertiesReturningCollections/cs/FxCop.Usage.PropertiesReturningCollections.cs#1)]
 [!code-vb[FxCop.Usage.PropertiesReturningCollections#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.PropertiesReturningCollections/vb/FxCop.Usage.PropertiesReturningCollections.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1819：属性不应返回数组](../code-quality/ca1819-properties-should-not-return-arrays.md)
