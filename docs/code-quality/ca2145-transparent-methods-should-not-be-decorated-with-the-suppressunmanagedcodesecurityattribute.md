---
title: CA2145:不应使用 SuppressUnmanagedCodeSecurityAttribute 修饰透明方法
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2145
ms.assetid: 81970700-b438-4b3b-9239-16887e16f7b7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3cca385c346a7daa8aaddb377f999506ffb1abaa
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232043"
---
# <a name="ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute"></a>CA2145:不应使用 SuppressUnmanagedCodeSecurityAttribute 修饰透明方法

|||
|-|-|
|TypeName|TransparentMethodsShouldNotUseSuppressUnmanagedCodeSecurity|
|CheckId|CA2145|
|类别|Microsoft.Security|
|重大更改|重大|

## <a name="cause"></a>原因

透明方法（用<xref:System.Security.SecuritySafeCriticalAttribute>方法标记的方法）或包含方法的类型<xref:System.Security.SuppressUnmanagedCodeSecurityAttribute>使用特性进行标记。

## <a name="rule-description"></a>规则说明

使用<xref:System.Security.SuppressUnmanagedCodeSecurityAttribute>特性修饰的方法在调用它的任何方法上都有一个隐式的 LinkDemand。 此 LinkDemand 要求调用代码是关键安全的。 标记将 SuppressUnmanagedCodeSecurity 与<xref:System.Security.SecurityCriticalAttribute>特性结合使用的方法，使此要求对于方法的调用方更为明显。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请使用<xref:System.Security.SecurityCriticalAttribute>特性标记方法或类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。

### <a name="code"></a>代码

[!code-csharp[FxCop.Security.CA2145.TransparentMethodsShouldNotUseSuppressUnmanagedCodeSecurity#1](../code-quality/codesnippet/CSharp/ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute_1.cs)]