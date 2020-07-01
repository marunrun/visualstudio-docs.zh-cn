---
title: CA2104：不要声明只读可变引用类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotDeclareReadOnlyMutableReferenceTypes
- CA2104
helpviewer_keywords:
- CA2104
- DoNotDeclareReadOnlyMutableReferenceTypes
ms.assetid: 81b83ee5-4db5-4be0-9f8d-90b53894ec3b
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ff42cc2b8543fe8e1cf980a3574ae15922febf9b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85521038"
---
# <a name="ca2104-do-not-declare-read-only-mutable-reference-types"></a>CA2104:不要声明只读可变引用类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|DoNotDeclareReadOnlyMutableReferenceTypes|
|CheckId|CA2104|
|类别|Microsoft.Security|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 外部可见类型包含外部可见的只读字段，该字段为可变的引用类型。

## <a name="rule-description"></a>规则描述
 可变类型是实例数据可被修改的类型。 <xref:System.Text.StringBuilder?displayProperty=fullName>类是可变引用类型的示例。 它包含可以更改类的实例值的成员。 类是不可变引用类型的一个示例 <xref:System.String?displayProperty=fullName> 。 在实例化后，其值永远不会更改。

 引用类型字段上的只读修饰符（c # 中为[readonly](https://msdn.microsoft.com/library/2f8081f6-0de2-4903-898d-99696c48d2f4) 、在 c + + 中为[readonly](https://msdn.microsoft.com/library/e868185d-6142-4359-a2fd-a7965cadfce8) [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 和[const](https://msdn.microsoft.com/library/b21c0271-1ad0-40a0-b21c-5e812bba0318) ）可防止该字段被引用类型的另一个实例替换。 但是，修饰符不会阻止通过引用类型修改字段的实例数据。

 只读数组字段不受此规则的阻止，而是导致 CA2105 的冲突[：数组字段不应为只读](../code-quality/ca2105-array-fields-should-not-be-read-only.md)规则。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请删除只读修饰符，或者，如果可接受重大更改，请将该字段替换为不可变类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果字段类型为不可变，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示了导致违反此规则的字段声明。

 [!code-cpp[FxCop.Security.MutableReferenceTypes#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.MutableReferenceTypes/cpp/FxCop.Security.MutableReferenceTypes.cpp#1)]
 [!code-csharp[FxCop.Security.MutableReferenceTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.MutableReferenceTypes/cs/FxCop.Security.MutableReferenceTypes.cs#1)]
 [!code-vb[FxCop.Security.MutableReferenceTypes#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.MutableReferenceTypes/vb/FxCop.Security.MutableReferenceTypes.vb#1)]
