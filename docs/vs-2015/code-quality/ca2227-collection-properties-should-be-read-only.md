---
title: CA2227:集合属性应为只读 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 3182a254ed5e22c560523911f87dc852708a9eb1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201582"
---
# <a name="ca2227-collection-properties-should-be-read-only"></a>CA2227:集合属性应为只读
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|CollectionPropertiesShouldBeReadOnly|
|CheckId|CA2227|
|类别|Microsoft.Usage|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见的可写属性是一种实现<xref:System.Collections.ICollection?displayProperty=fullName>。 规则将忽略数组、 索引器 （使用名为 Item 的属性） 和权限集。

## <a name="rule-description"></a>规则说明
 可写集合属性允许用户替换为完全不同的集合的集合。 只读属性禁止替换该集合，但仍允许设置单个成员。 如果替换该集合是一个目标，首选的设计模式是包括用于删除集合中的所有元素的方法和方法来重新填充该集合。 请参阅<xref:System.Collections.ArrayList.Clear%2A>并<xref:System.Collections.ArrayList.AddRange%2A>方法的<xref:System.Collections.ArrayList?displayProperty=fullName>有关此模式的示例类。

 二进制和 XML 序列化支持是集合的只读属性。 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName>类具有实现的类型的特定要求<xref:System.Collections.ICollection>和<xref:System.Collections.IEnumerable?displayProperty=fullName>为了可序列化。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，使该属性只读，并设计需要它，如果添加用于清除和重新填充该集合的方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例显示具有可写集合属性的类型，并显示如何直接替换集合。 此外，替换只读集合属性中使用的首选的方式`Clear`和`AddRange`方法所示。

 [!code-cpp[FxCop.Usage.PropertiesReturningCollections#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.PropertiesReturningCollections/cpp/FxCop.Usage.PropertiesReturningCollections.cpp#1)]
 [!code-csharp[FxCop.Usage.PropertiesReturningCollections#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.PropertiesReturningCollections/cs/FxCop.Usage.PropertiesReturningCollections.cs#1)]
 [!code-vb[FxCop.Usage.PropertiesReturningCollections#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.PropertiesReturningCollections/vb/FxCop.Usage.PropertiesReturningCollections.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA1819:属性不应返回数组](../code-quality/ca1819-properties-should-not-return-arrays.md)
