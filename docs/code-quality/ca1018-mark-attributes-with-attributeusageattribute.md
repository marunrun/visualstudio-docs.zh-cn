---
title: CA1018:用 AttributeUsageAttribute 标记特性
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1018
- MarkAttributesWithAttributeUsage
helpviewer_keywords:
- CA1018
- MarkAttributesWithAttributeUsage
ms.assetid: 6ab70ec0-220f-4880-af31-45067703133c
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 133ee073398817c037af95e2009c5acc98e1e5a2
ms.sourcegitcommit: 034c503ae04e22cf840ccb9770bffd012e40fb2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2019
ms.locfileid: "72306132"
---
# <a name="ca1018-mark-attributes-with-attributeusageattribute"></a>CA1018:用 AttributeUsageAttribute 标记特性

|||
|-|-|
|TypeName|MarkAttributesWithAttributeUsage|
|CheckId|CA1018|
|类别|Microsoft.Design|
|重大更改|重大|

## <a name="cause"></a>原因
自定义属性上不存在 <xref:System.AttributeUsageAttribute?displayProperty=fullName> 属性。

## <a name="rule-description"></a>规则说明
定义自定义属性时，请使用 <xref:System.AttributeUsageAttribute> 来标记该自定义属性，以便在源代码中指定自定义属性的应用位置。 特性的含义和预定用法将决定它在代码中的有效位置。 例如，你可以定义一个属性，该属性标识负责维护和增强库中的每个类型的人员，并且始终在类型级别分配责任。 在这种情况下，编译器应启用类、枚举和接口上的属性，但不应在方法、事件或属性上启用它。 组织策略和过程将规定是否应在程序集上启用该属性。

@No__t-0 枚举定义可为自定义属性指定的目标。 如果省略 <xref:System.AttributeUsageAttribute>，自定义属性将对所有目标有效，如 <xref:System.AttributeTargets> 枚举的 `All` 值所定义。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请使用 @no__t 为属性指定目标。 请参见以下示例。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
应修复与此规则的冲突，而不是排除消息。 即使属性继承 <xref:System.AttributeUsageAttribute>，也应该提供属性以简化代码维护。

## <a name="example"></a>示例
下面的示例定义了两个特性。 `BadCodeMaintainerAttribute` 错误地省略了 @no__t 1 语句，`GoodCodeMaintainerAttribute` 正确实现了本部分前面所述的属性。 请注意，设计规则 [CA1019 需要属性 `DeveloperName`：为属性参数 @ no__t 定义访问器，出于完整性考虑，将包括在内。

[!code-csharp[FxCop.Design.AttributeUsage#1](../code-quality/codesnippet/CSharp/ca1018-mark-attributes-with-attributeusageattribute_1.cs)]
[!code-vb[FxCop.Design.AttributeUsage#1](../code-quality/codesnippet/VisualBasic/ca1018-mark-attributes-with-attributeusageattribute_1.vb)]

## <a name="related-rules"></a>相关规则
[CA1019：定义特性参数的访问器 @ no__t-0

[CA1813：避免未密封的属性 @ no__t

## <a name="see-also"></a>请参阅

- [属性](/dotnet/standard/design-guidelines/attributes)