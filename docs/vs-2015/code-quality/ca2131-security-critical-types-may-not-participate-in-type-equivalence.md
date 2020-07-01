---
title: CA2131：安全关键类型不能参与类型等效性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2131
ms.assetid: 4170f3b1-6086-430d-8fba-837d5538c573
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ccd556a5929e56597de678ad4ad8ea6c101b7c7f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535884"
---
# <a name="ca2131-security-critical-types-may-not-participate-in-type-equivalence"></a>CA2131:安全关键类型不能参与类型等效
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|CriticalTypesMustNotParticipateInTypeEquivalence|
|CheckId|CA2131|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 类型参与类型等效，而类型本身或类型的成员或字段均使用特性进行标记 <xref:System.Security.SecurityCriticalAttribute> 。

## <a name="rule-description"></a>规则描述
 对于任何关键的类型或包含参与类型等效的关键方法或字段的类型，将引发此规则。 当 CLR 检测到此类类型时，它无法 <xref:System.TypeLoadException> 在运行时加载它。 通常，仅在用户手动实现类型等效而不是通过依赖 tlbimp 和编译器进行类型等效时，才会触发此规则。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请删除 SecurityCritical 属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示了一个接口、一个方法和一个将导致此规则激发的字段。

 [!code-csharp[FxCop.Security.CA2131.CriticalTypesMustNotParticipateInTypeEquivalence#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2131.criticaltypesmustnotparticipateintypeequivalence/cs/ca2131 - criticaltypesmustnotparticipateintypeequivalence.cs#1)]

## <a name="see-also"></a>另请参阅
 [安全透明的代码，级别 2](https://msdn.microsoft.com/library/4d05610a-0da6-4f08-acea-d54c9d6143c0)
