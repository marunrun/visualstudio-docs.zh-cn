---
title: CA2136：成员不应有相互冲突的透明度批注 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2127
- SecurityTransparentAssembliesShouldNotContainSecurityCriticalCode
- CA2136
helpviewer_keywords:
- SecurityTransparentAssembliesShouldNotContainSecurityCriticalCode
- CA2127
ms.assetid: ff5a1d18-7c52-4da5-8990-60be83a8ea81
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f2fbb856ff53552ab99dabd4f650e9fd7f62a088
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72602972"
---
# <a name="ca2136-members-should-not-have-conflicting-transparency-annotations"></a>CA2136：成员不应有相互冲突的透明度注释
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|TransparencyAnnotationsShouldNotConflict|
|CheckId|CA2136|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 当类型成员标记为具有与成员容器的安全属性不同的透明度 <xref:System.Security> 安全特性时，将触发此规则。

## <a name="rule-description"></a>规则说明
 将透明特性从较大作用域的代码元素应用到较小作用域的元素。 具有较大作用域的代码元素的透明特性优于第一个元素中包含的代码元素的透明特性。 例如，使用 <xref:System.Security.SecurityCriticalAttribute> 特性标记的类不能包含用 <xref:System.Security.SecuritySafeCriticalAttribute> 特性标记的方法。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此冲突，请从包含较低范围的代码元素中移除安全特性，或将其特性更改为与包含代码元素相同。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 请勿禁止显示此规则的警告。

## <a name="example"></a>示例
 在下面的示例中，使用 <xref:System.Security.SecuritySafeCriticalAttribute> 特性标记了一个方法，该方法是使用 <xref:System.Security.SecurityCriticalAttribute> 特性标记的类的成员。 应删除安全安全特性。

 [!code-csharp[FxCop.Security.CA2136.TransparencyAnnotationsShouldNotConflict#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2136.transparencyannotationsshouldnotconflict/cs/ca2136 - transparencyannotationsshouldnotconflict.cs#1)]
