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
ms.openlocfilehash: be864812cc7355f80700bd3e270178c9626d4180
ms.sourcegitcommit: 034c503ae04e22cf840ccb9770bffd012e40fb2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305897"
---
# <a name="ca2227-collection-properties-should-be-read-only"></a>CA2227:集合属性应为只读

|||
|-|-|
|TypeName|CollectionPropertiesShouldBeReadOnly|
|CheckId|CA2227|
|类别|Microsoft.Usage|
|重大更改|重大|

## <a name="cause"></a>原因

外部可见、可写的属性属于实现 <xref:System.Collections.ICollection?displayProperty=fullName> 的类型。 此规则将忽略数组、索引器（名称为 "Item" 的属性）和权限集。

## <a name="rule-description"></a>规则说明

可写集合属性允许用户将集合替换为完全不同的集合。 只读属性会阻止集合被替换，但仍允许设置单个成员。 如果替换集合是一个目标，则首选的设计模式是包含用于从集合中移除所有元素的方法，以及用于重新填充集合的方法。 有关此模式的示例，请参阅 <xref:System.Collections.ArrayList?displayProperty=fullName> 类的 <xref:System.Collections.ArrayList.Clear%2A> 和 @no__t 方法。

二进制和 XML 序列化都支持作为集合的只读属性。 @No__t-0 类对于实现 @no__t 和 @no__t 为可序列化的类型具有特定的要求。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请将属性设置为只读。 如果设计需要它，请添加方法以清除和重新填充集合。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果该属性是[数据传输对象（DTO）](/previous-versions/msp-n-p/ff649585(v=pandp.10))类的一部分，则可以禁止显示该警告。

否则，请勿禁止显示此规则的警告。

## <a name="example"></a>示例

下面的示例演示一个具有可写集合属性的类型，并演示如何直接替换该集合。 此外，它还显示了使用 @no__t 0 和 @no__t 1 方法替换只读集合属性的首选方式。

[!code-csharp[FxCop.Usage.PropertiesReturningCollections#1](../code-quality/codesnippet/CSharp/ca2227-collection-properties-should-be-read-only_1.cs)]
[!code-vb[FxCop.Usage.PropertiesReturningCollections#1](../code-quality/codesnippet/VisualBasic/ca2227-collection-properties-should-be-read-only_1.vb)]
[!code-cpp[FxCop.Usage.PropertiesReturningCollections#1](../code-quality/codesnippet/CPP/ca2227-collection-properties-should-be-read-only_1.cpp)]

## <a name="related-rules"></a>相关规则

- [CA1819：属性不应返回数组 @ no__t-0