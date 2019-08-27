---
title: CA1813:避免使用非密封特性
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1813
- AvoidUnsealedAttributes
helpviewer_keywords:
- CA1813
- AvoidUnsealedAttributes
ms.assetid: f5e31b4c-9f8b-49e1-a2a8-bb5f1140729a
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: a17c5bdc9e21bdf877206b1dc28596c251049455
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66714745"
---
# <a name="ca1813-avoid-unsealed-attributes"></a>CA1813:避免使用非密封特性

|||
|-|-|
|TypeName|AvoidUnsealedAttributes|
|CheckId|CA1813|
|类别|Microsoft.Performance|
|是否重大更改|重大|

## <a name="cause"></a>原因

公共类型都继承<xref:System.Attribute?displayProperty=fullName>、 不是抽象的并且未密封 (`NotInheritable`在 Visual Basic 中)。

## <a name="rule-description"></a>规则说明

.NET 提供了用于检索自定义特性的方法。 默认情况下，这些方法搜索特性继承层次结构。 例如，<xref:System.Attribute.GetCustomAttribute%2A?displayProperty=fullName>搜索指定的特性类型或任何扩展指定的特性类型的属性类型。 密封特性无需通过继承层次结构中，搜索并提高性能。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要解决此规则的冲突，密封特性类型或使其成为抽象类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

它可以安全地禁止显示此规则的警告。 禁止显示仅当要定义属性层次结构和不能密封特性或使其成为抽象。

## <a name="example"></a>示例

下面的示例显示了满足此规则的自定义属性。

[!code-csharp[FxCop.Performance.AttributesSealed#1](../code-quality/codesnippet/CSharp/ca1813-avoid-unsealed-attributes_1.cs)]
[!code-vb[FxCop.Performance.AttributesSealed#1](../code-quality/codesnippet/VisualBasic/ca1813-avoid-unsealed-attributes_1.vb)]

## <a name="related-rules"></a>相关的规则

- [CA1019:定义特性参数的访问器](../code-quality/ca1019-define-accessors-for-attribute-arguments.md)
- [CA1018:用 AttributeUsageAttribute 标记特性](../code-quality/ca1018-mark-attributes-with-attributeusageattribute.md)

## <a name="see-also"></a>请参阅

- [属性](/dotnet/standard/design-guidelines/attributes)