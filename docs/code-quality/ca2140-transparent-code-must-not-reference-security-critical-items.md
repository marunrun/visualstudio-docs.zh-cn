---
title: CA2140:透明代码不得引用安全关键项
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2129
- SecurityTransparentCodeShouldNotReferenceNonpublicSecurityCriticalCode
- CA2140
helpviewer_keywords:
- CA2140
- SecurityTransparentCodeShouldNotReferenceNonpublicSecurityCriticalCode
- CA2129
ms.assetid: 251a12da-0557-47f5-a4f7-0229d590ae7b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d4f02938aed7456762f1ef51da716b6b96bdf437
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232151"
---
# <a name="ca2140-transparent-code-must-not-reference-security-critical-items"></a>CA2140:透明代码不得引用安全关键项

|||
|-|-|
|TypeName|TransparentMethodsMustNotReferenceCriticalCode|
|CheckId|CA2140|
|类别|Microsoft.Security|
|重大更改|重大|

## <a name="cause"></a>原因

透明方法：

- 处理安全关键安全异常类型

- 具有标记为安全关键类型的参数

- 具有包含安全关键约束的泛型参数

- 具有安全关键类型的局部变量

- 引用标记为安全关键的类型

- 调用标记为 "安全关键" 的方法

- 引用标记为安全关键的字段

- 返回标记为安全关键的类型

## <a name="rule-description"></a>规则说明

用<xref:System.Security.SecurityCriticalAttribute>特性标记的代码元素是安全关键的。 透明方法不能使用安全关键元素。 如果透明类型尝试使用安全关键类型<xref:System.TypeAccessException>，则会引发、 <xref:System.MethodAccessException>或。 <xref:System.FieldAccessException>

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请执行以下操作之一：

- 标记使用带有<xref:System.Security.SecurityCriticalAttribute>特性的安全关键代码的代码元素

     \- 或 -

- 从标记为 "安全关键" 的代码元素删除<xref:System.Security.SecuritySafeCriticalAttribute> <xref:System.Security.SecurityTransparentAttribute> 属性，并将其标记<xref:System.Security.SecurityCriticalAttribute>为或属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。

## <a name="example"></a>示例

在下面的示例中，透明方法尝试引用安全关键的泛型集合、安全关键的字段和安全关键方法。

[!code-csharp[FxCop.Security.CA2140.TransparentMethodsMustNotReferenceCriticalCode#1](../code-quality/codesnippet/CSharp/ca2140-transparent-code-must-not-reference-security-critical-items_1.cs)]

## <a name="see-also"></a>请参阅

- <xref:System.Security.SecurityTransparentAttribute>
- <xref:System.Security.SecurityCriticalAttribute>
- <xref:System.Security.SecurityTransparentAttribute>
- <xref:System.Security.SecurityTreatAsSafeAttribute>
- <xref:System.Security?displayProperty=fullName>