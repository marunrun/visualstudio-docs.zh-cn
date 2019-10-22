---
title: CA1813：避免未密封的属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1813
- AvoidUnsealedAttributes
helpviewer_keywords:
- CA1813
- AvoidUnsealedAttributes
ms.assetid: f5e31b4c-9f8b-49e1-a2a8-bb5f1140729a
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: fe5967ef099794b6c71029e9d03d959dd83b01dc
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72647055"
---
# <a name="ca1813-avoid-unsealed-attributes"></a>CA1813：避免使用未密封的特性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidUnsealedAttributes|
|CheckId|CA1813|
|类别|Microsoft. 性能|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共类型从 <xref:System.Attribute?displayProperty=fullName> 继承，不是抽象的，并且不是密封的（`NotInheritable` Visual Basic）。

## <a name="rule-description"></a>规则说明
 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 类库提供用于检索自定义特性的方法。 默认情况下，这些方法在属性继承层次结构中搜索;例如 <xref:System.Attribute.GetCustomAttribute%2A?displayProperty=fullName> 搜索指定的属性类型或任何扩展指定属性类型的属性类型。 密封属性可在继承层次结构中消除搜索，并可提高性能。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请密封属性类型或使其成为抽象类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 可以安全地禁止显示此规则发出的警告。 仅当定义属性层次结构，并且不能密封属性或使其成为抽象属性时，才应执行此操作。

## <a name="example"></a>示例
 下面的示例演示一个满足此规则的自定义属性。

 [!code-csharp[FxCop.Performance.AttributesSealed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.AttributesSealed/cs/FxCop.Performance.AttributesSealed.cs#1)]
 [!code-vb[FxCop.Performance.AttributesSealed#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.AttributesSealed/vb/FxCop.Performance.AttributesSealed.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1019：定义特性参数的访问器](../code-quality/ca1019-define-accessors-for-attribute-arguments.md)

 [CA1018：用 AttributeUsageAttribute 标记特性](../code-quality/ca1018-mark-attributes-with-attributeusageattribute.md)

## <a name="see-also"></a>请参阅
 [特性](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b)
