---
title: CA2146:类型必须至少与其基类型和接口一样关键
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2146
ms.assetid: 241fb784-1f6b-46e5-8ceb-c438e341d38e
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a70e999505bd900a7b3d89693ef4f6a1cef9de7d
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920424"
---
# <a name="ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces"></a>CA2146:类型必须至少与其基类型和接口一样关键

|||
|-|-|
|TypeName|TypesMustBeAtLeastAsCriticalAsBaseTypes|
|CheckId|CA2146|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
透明<xref:System.Security.SecuritySafeCriticalAttribute>类型是从用<xref:System.Security.SecurityCriticalAttribute>或标记的类型派生的, 或者使用<xref:System.Security.SecuritySafeCriticalAttribute>特性标记的类型派生<xref:System.Security.SecurityCriticalAttribute>自使用特性标记的类型。

## <a name="rule-description"></a>规则说明
当派生类型具有的安全透明特性与其基类型或实现的接口不是同样关键时，将引发此规则。 只有关键类型可以从关键基类型派生或实现关键接口，并且只有关键或关键安全类型可以从安全关键基类型派生或实现关键安全接口。 在第2级透明度中违反此规则会导致<xref:System.TypeLoadException>派生类型的。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要解决此冲突, 请使用与基类型或接口至少相同的透明度特性标记派生的或实现类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
[!code-csharp[FxCop.Security.CA2146.TypesMustBeAtLeastAsCriticalAsBaseTypes#1](../code-quality/codesnippet/CSharp/ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces_1.cs)]