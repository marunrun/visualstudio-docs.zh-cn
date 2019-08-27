---
title: CA2227:集合属性应为只读
ms.date: 09/28/2018
ms.topic: reference
f1_keywords:
- CA2227
- CollectionPropertiesShouldBeReadOnly
helpviewer_keywords:
- CA2227
- CollectionPropertiesShouldBeReadOnly
ms.assetid: 26967aaf-6fbe-438a-b4d3-ac579b5dc0f9
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.openlocfilehash: 8a6ced277aa442450418ce55f4e1db56ad5d8af1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806532"
---
# <a name="ca2227-collection-properties-should-be-read-only"></a>CA2227:集合属性应为只读

|||
|-|-|
|TypeName|CollectionPropertiesShouldBeReadOnly|
|CheckId|CA2227|
|类别|Microsoft.Usage|
|是否重大更改|重大|

## <a name="cause"></a>原因

外部可见，则可写属性的实现的类型是<xref:System.Collections.ICollection?displayProperty=fullName>。 数组、 索引器 （使用名为 Item 的属性） 和权限集，将忽略此规则。

## <a name="rule-description"></a>规则说明

可写集合属性允许用户替换为完全不同的集合的集合。 只读属性停止从被替换的集合，但仍然允许各个成员进行设置。 如果替换该集合是一个目标，首选的设计模式是包括用于从集合中移除所有元素的方法和方法来重新填充集合。 请参阅<xref:System.Collections.ArrayList.Clear%2A>并<xref:System.Collections.ArrayList.AddRange%2A>方法的<xref:System.Collections.ArrayList?displayProperty=fullName>有关此模式的示例类。

二进制和 XML 序列化支持是集合的只读属性。 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName>类具有实现的类型的特定要求<xref:System.Collections.ICollection>和<xref:System.Collections.IEnumerable?displayProperty=fullName>为了可序列化。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要解决此规则的冲突，使属性成为只读的。 如果设计需要它，将添加用于清除和重新填充集合的方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果该属性的一部分，可以禁止显示警告[数据传输对象 (DTO)](/previous-versions/msp-n-p/ff649585(v=pandp.10))类。

否则，不要禁止显示此规则的警告。

## <a name="example"></a>示例

下面的示例显示具有可写集合属性的类型，并显示如何直接替换集合。 此外，它显示的替换为只读集合属性中使用的首选的方式`Clear`和`AddRange`方法。

[!code-csharp[FxCop.Usage.PropertiesReturningCollections#1](../code-quality/codesnippet/CSharp/ca2227-collection-properties-should-be-read-only_1.cs)]
[!code-vb[FxCop.Usage.PropertiesReturningCollections#1](../code-quality/codesnippet/VisualBasic/ca2227-collection-properties-should-be-read-only_1.vb)]
[!code-cpp[FxCop.Usage.PropertiesReturningCollections#1](../code-quality/codesnippet/CPP/ca2227-collection-properties-should-be-read-only_1.cpp)]

## <a name="related-rules"></a>相关的规则

- [CA1819:属性不应返回数组](../code-quality/ca1819-properties-should-not-return-arrays.md)