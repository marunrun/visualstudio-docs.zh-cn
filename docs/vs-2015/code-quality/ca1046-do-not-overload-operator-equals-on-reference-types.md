---
title: CA1046:请重载相等运算符对引用类型 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: c2d9e301b842e0cbd84e23b58310c6afad276b4a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696765"
---
# <a name="ca1046-do-not-overload-operator-equals-on-reference-types"></a>CA1046:不要对引用类型重载相等运算符
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotOverloadOperatorEqualsOnReferenceTypes|
|CheckId|CA1046|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或嵌套公共引用类型重载相等运算符。

## <a name="rule-description"></a>规则说明
 对于引用类型，相等运算符的默认实现几乎始终是正确的。 默认情况下，仅当两个引用指向同一对象时，它们才相等。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请删除相等运算符的实现。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告时引用类型的行为类似于内置值类型。 如果它是类型的有意义，若要执行相加或相减实例，则可能是类型的正确实现相等运算符，并禁止显示冲突。

## <a name="example"></a>示例
 比较两个引用时，下面的示例演示默认行为。

 [!code-csharp[FxCop.Design.RefTypesNoEqualityOp#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.RefTypesNoEqualityOp/cs/FxCop.Design.RefTypesNoEqualityOp.cs#1)]

## <a name="example"></a>示例
 下面的应用程序将一些引用进行比较。

 [!code-csharp[FxCop.Design.TestRefTypesNoEqualityOp#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestRefTypesNoEqualityOp/cs/FxCop.Design.TestRefTypesNoEqualityOp.cs#1)]

 本示例生成以下输出。

 **= 新 (2，2) 且 b = 新 (2，2) 是否相等？否**
**c 和 a 为相等？是**
**b 和 a = =？否**
**c 和 a = =？是的**
## <a name="related-rules"></a>相关的规则
 [CA1013:重载相等运算符，加法和减法](../code-quality/ca1013-overload-operator-equals-on-overloading-add-and-subtract.md)

## <a name="see-also"></a>请参阅
 <xref:System.Object.Equals%2A?displayProperty=fullName> [相等运算符](https://msdn.microsoft.com/library/bc496a91-fefb-4ce0-ab4c-61f09964119a)
