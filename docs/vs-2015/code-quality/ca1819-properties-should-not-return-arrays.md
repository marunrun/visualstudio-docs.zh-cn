---
title: CA1819：属性不应返回数组 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PropertiesShouldNotReturnArrays
- CA1819
helpviewer_keywords:
- PropertiesShouldNotReturnArrays
- CA1819
ms.assetid: 85fcf312-57f8-438a-8b10-34441fe0bdeb
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5c85efc3e601eb9e0d887043c50b30587e51321e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668379"
---
# <a name="ca1819-properties-should-not-return-arrays"></a>CA1819：属性不应返回数组
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|PropertiesShouldNotReturnArrays|
|CheckId|CA1819|
|类别|Microsoft. 性能|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共类型中的公共或受保护的属性返回一个数组。

## <a name="rule-description"></a>规则说明
 即使属性是只读的，由属性返回的数组仍不受写保护。 若要使数组不会被更改，属性必须返回数组的副本。 通常，用户不能理解调用这种属性的负面性能影响。 具体说来，它们可能使用属性作为索引属性。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将属性设置为方法或更改属性以返回集合。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 特性可以包含返回数组的属性，但不能包含返回集合的属性。 您可以禁止显示从 [System.object] 派生的属性的属性引发的警告（<!-- TODO: review code entity reference <xref:assetId:///System.Attribute?qualifyHint=False&amp;autoUpgrade=True>  -->班级. 否则，请不要禁止显示此规则发出的警告。

## <a name="example-violation"></a>示例冲突

### <a name="description"></a>描述
 下面的示例演示了与此规则冲突的属性。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Performance.PropertyArrayViolation#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayViolation/cs/FxCop.Performance.PropertyArrayViolation.cs#1)]
 [!code-vb[FxCop.Performance.PropertyArrayViolation#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayViolation/vb/FxCop.Performance.PropertyArrayViolation.vb#1)]

### <a name="comments"></a>注释
 若要修复与此规则的冲突，请将属性设置为方法或更改属性以返回集合而不是数组。

## <a name="change-the-property-to-a-method-example"></a>将属性更改为方法示例

### <a name="description"></a>描述
 下面的示例通过将属性更改为方法来修复冲突。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Performance.PropertyArrayFixedMethod#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayFixedMethod/cs/FxCop.Performance.PropertyArrayFixedMethod.cs#1)]
 [!code-vb[FxCop.Performance.PropertyArrayFixedMethod#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayFixedMethod/vb/FxCop.Performance.PropertyArrayFixedMethod.vb#1)]

## <a name="return-a-collection-example"></a>返回集合示例

### <a name="description"></a>描述
 下面的示例通过将属性更改为返回

 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=fullName>

### <a name="code"></a>代码
 [!code-csharp[FxCop.Performance.PropertyArrayFixedCollection#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayFixedCollection/cs/FxCop.Performance.PropertyArrayFixedCollection.cs#1)]
 [!code-vb[FxCop.Performance.PropertyArrayFixedCollection#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayFixedCollection/vb/FxCop.Performance.PropertyArrayFixedCollection.vb#1)]

## <a name="allowing-users-to-modify-a-property"></a>允许用户修改属性

### <a name="description"></a>描述
 您可能希望允许类的使用者修改属性。 下面的示例演示了违反此规则的读/写属性。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Performance.PropertyModifyViolation#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyModifyViolation/cs/FxCop.Performance.PropertyModifyViolation.cs#1)]
 [!code-vb[FxCop.Performance.PropertyModifyViolation#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyModifyViolation/vb/FxCop.Performance.PropertyModifyViolation.vb#1)]

### <a name="comments"></a>注释
 下面的示例通过更改属性来返回 <xref:System.Collections.ObjectModel.Collection%601?displayProperty=fullName> 来修复冲突。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Performance.PropertyModifyFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyModifyFixed/cs/FxCop.Performance.PropertyModifyFixed.cs#1)]
 [!code-vb[FxCop.Performance.PropertyModifyFixed#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyModifyFixed/vb/FxCop.Performance.PropertyModifyFixed.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1024：在适用处使用属性](../code-quality/ca1024-use-properties-where-appropriate.md)
