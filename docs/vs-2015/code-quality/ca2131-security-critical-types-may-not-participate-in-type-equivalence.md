---
title: CA2131:安全关键类型不能参与类型等效性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2131
ms.assetid: 4170f3b1-6086-430d-8fba-837d5538c573
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 6fba07fbfd7f0c36681b7567ad01359df1be88f6
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65700523"
---
# <a name="ca2131-security-critical-types-may-not-participate-in-type-equivalence"></a>CA2131:安全关键类型不能参与类型等效
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|CriticalTypesMustNotParticipateInTypeEquivalence|
|CheckId|CA2131|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 某个类型参与类型等效性和该类型本身，或用标记的成员或字段的类型，<xref:System.Security.SecurityCriticalAttribute>属性。

## <a name="rule-description"></a>规则说明
 对于任何关键的类型或包含参与类型等效的关键方法或字段的类型，将引发此规则。 当 CLR 检测到这种类型时，它会加载它与<xref:System.TypeLoadException>在运行时。 通常，仅在用户手动实现类型等效而不是通过依赖 tlbimp 和编译器进行类型等效时，才会触发此规则。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请删除 SecurityCritical 属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 以下示例演示一个接口、 方法和字段将导致触发此规则。

 [!code-csharp[FxCop.Security.CA2131.CriticalTypesMustNotParticipateInTypeEquivalence#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2131.criticaltypesmustnotparticipateintypeequivalence/cs/ca2131 - criticaltypesmustnotparticipateintypeequivalence.cs#1)]

## <a name="see-also"></a>请参阅
 [安全透明代码，级别 2](https://msdn.microsoft.com/library/4d05610a-0da6-4f08-acea-d54c9d6143c0)
