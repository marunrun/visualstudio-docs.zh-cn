---
title: CA1018：用 AttributeUsageAttribute 标记特性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1018
- MarkAttributesWithAttributeUsage
helpviewer_keywords:
- CA1018
- MarkAttributesWithAttributeUsage
ms.assetid: 6ab70ec0-220f-4880-af31-45067703133c
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 404ef250726d12300e2b72150ff42b4f0b7bfb24
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662054"
---
# <a name="ca1018-mark-attributes-with-attributeusageattribute"></a>CA1018：用 AttributeUsageAttribute 标记特性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MarkAttributesWithAttributeUsage|
|CheckId|CA1018|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 自定义属性上不存在 <xref:System.AttributeUsageAttribute?displayProperty=fullName> 特性。

## <a name="rule-description"></a>规则说明
 定义自定义属性时，请使用 <xref:System.AttributeUsageAttribute> 来标记该自定义属性，以指示在源代码中可以应用自定义属性的位置。 特性的含义和预定用法将决定它在代码中的有效位置。 例如，你可以定义一个属性，该属性标识负责维护和增强库中的每个类型的人员，并且始终在类型级别分配责任。 在这种情况下，编译器应启用类、枚举和接口上的属性，但不应在方法、事件或属性上启用它。 组织策略和过程将规定是否应在程序集上启用该属性。

 @No__t_0 枚举定义可为自定义属性指定的目标。 如果省略 <xref:System.AttributeUsageAttribute>，自定义属性将对所有目标有效，如 <xref:System.AttributeTargets> 枚举的 `All` 值所定义。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请使用 <xref:System.AttributeUsageAttribute> 指定属性的目标。 请参见以下示例。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 应修复与此规则的冲突，而不是排除消息。 即使属性继承 <xref:System.AttributeUsageAttribute>，属性也应存在，以简化代码维护。

## <a name="example"></a>示例
 下面的示例定义了两个特性。 `BadCodeMaintainerAttribute` 错误地省略了 <xref:System.AttributeUsageAttribute> 语句，`GoodCodeMaintainerAttribute` 正确实现本部分前面所述的属性。 请注意，设计规则[CA1019：定义特性参数的访问器](../code-quality/ca1019-define-accessors-for-attribute-arguments.md)时，属性 `DeveloperName` 是必需的，出于完整性考虑，它包括在内。

 [!code-csharp[FxCop.Design.AttributeUsage#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeUsage/cs/FxCop.Design.AttributeUsage.cs#1)]
 [!code-vb[FxCop.Design.AttributeUsage#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeUsage/vb/FxCop.Design.AttributeUsage.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1019：定义特性参数的访问器](../code-quality/ca1019-define-accessors-for-attribute-arguments.md)

 [CA1813：避免使用未密封的特性](../code-quality/ca1813-avoid-unsealed-attributes.md)

## <a name="see-also"></a>请参阅
 [特性](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b)
