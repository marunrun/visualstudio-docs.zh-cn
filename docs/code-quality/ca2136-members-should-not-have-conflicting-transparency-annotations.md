---
title: CA2136:成员不应具有冲突的透明度批注
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2127
- SecurityTransparentAssembliesShouldNotContainSecurityCriticalCode
- CA2136
helpviewer_keywords:
- SecurityTransparentAssembliesShouldNotContainSecurityCriticalCode
- CA2127
ms.assetid: ff5a1d18-7c52-4da5-8990-60be83a8ea81
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7f9455e83d7cb128a34696ae5e849fd0901f1891
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232222"
---
# <a name="ca2136-members-should-not-have-conflicting-transparency-annotations"></a>CA2136:成员不应具有冲突的透明度批注

|||
|-|-|
|TypeName|TransparencyAnnotationsShouldNotConflict|
|CheckId|CA2136|
|类别|Microsoft.Security|
|重大更改|重大|

## <a name="cause"></a>原因
当类型成员标记<xref:System.Security>为具有与成员容器的安全属性不同的透明度的安全特性时，将触发此规则。

## <a name="rule-description"></a>规则说明
将透明特性从较大作用域的代码元素应用到较小作用域的元素。 具有较大作用域的代码元素的透明特性优于第一个元素中包含的代码元素的透明特性。 例如，用<xref:System.Security.SecurityCriticalAttribute>特性标记的类不能包含<xref:System.Security.SecuritySafeCriticalAttribute>用特性标记的方法。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要解决此冲突，请从包含较低范围的代码元素中移除安全特性，或将其特性更改为与包含代码元素相同。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
请勿禁止显示此规则的警告。

## <a name="example"></a>示例
在下面的示例中，用<xref:System.Security.SecuritySafeCriticalAttribute>特性标记方法，并且它是<xref:System.Security.SecurityCriticalAttribute>用特性标记的类的成员。 应删除安全安全特性。

[!code-csharp[FxCop.Security.CA2136.TransparencyAnnotationsShouldNotConflict#1](../code-quality/codesnippet/CSharp/ca2136-members-should-not-have-conflicting-transparency-annotations_1.cs)]