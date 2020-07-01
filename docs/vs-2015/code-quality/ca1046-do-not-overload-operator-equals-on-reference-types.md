---
title: CA1046：不对引用类型重载运算符 equals |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotOverloadOperatorEqualsOnReferenceTypes
- CA1046
helpviewer_keywords:
- CA1046
- DoNotOverloadOperatorEqualsOnReferenceTypes
ms.assetid: c1dfbfe3-63f9-4005-a81a-890427b77e79
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 118c29473db09d5ed0a4fa447e27e593a88f98b3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546752"
---
# <a name="ca1046-do-not-overload-operator-equals-on-reference-types"></a>CA1046:不要对引用类型重载相等运算符
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|DoNotOverloadOperatorEqualsOnReferenceTypes|
|CheckId|CA1046|
|Category|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或嵌套公共引用类型重载相等运算符。

## <a name="rule-description"></a>规则描述
 对于引用类型，相等运算符的默认实现几乎始终是正确的。 默认情况下，仅当两个引用指向同一对象时，它们才相等。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请删除相等运算符的实现。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 当引用类型的行为与内置值类型相同时，可以安全地禁止显示此规则发出的警告。 如果在该类型的实例上执行加法或减法运算是有意义的，则实现相等运算符并取消此冲突可能是正确的。

## <a name="example"></a>示例
 下面的示例演示了在比较两个引用时的默认行为。

 [!code-csharp[FxCop.Design.RefTypesNoEqualityOp#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.RefTypesNoEqualityOp/cs/FxCop.Design.RefTypesNoEqualityOp.cs#1)]

## <a name="example"></a>示例
 以下应用程序比较一些引用。

 [!code-csharp[FxCop.Design.TestRefTypesNoEqualityOp#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestRefTypesNoEqualityOp/cs/FxCop.Design.TestRefTypesNoEqualityOp.cs#1)]

 本示例生成以下输出。

 **a = new （2，2）和 b = new （2，2）是否相同？没有** 
 **c 和 a 是否相等？是** 
 **b，a 是 = =？没有** 
 **c 和 a 是 = =？是**
## <a name="related-rules"></a>相关规则
 [CA1013:重载加法方法和减法方法时重载相等运算符](../code-quality/ca1013-overload-operator-equals-on-overloading-add-and-subtract.md)

## <a name="see-also"></a>另请参阅
 <xref:System.Object.Equals%2A?displayProperty=fullName>[相等运算符](https://msdn.microsoft.com/library/bc496a91-fefb-4ce0-ab4c-61f09964119a)
