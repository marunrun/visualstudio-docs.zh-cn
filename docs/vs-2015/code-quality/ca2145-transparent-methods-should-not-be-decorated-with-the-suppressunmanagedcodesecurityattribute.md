---
title: CA2145：不应通过 SuppressUnmanagedCodeSecurityAttribute 修饰透明方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2145
ms.assetid: 81970700-b438-4b3b-9239-16887e16f7b7
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d5eb16130aef42abcf9fddf533d0253864a75114
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546401"
---
# <a name="ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute"></a>CA2145:不应使用 SuppressUnmanagedCodeSecurityAttribute 修饰透明方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|TransparentMethodsShouldNotUseSuppressUnmanagedCodeSecurity|
|CheckId|CA2145|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 透明方法（用方法标记的方法 <xref:System.Security.SecuritySafeCriticalAttribute> ）或包含方法的类型使用特性进行标记 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> 。

## <a name="rule-description"></a>规则描述
 使用特性修饰的方法在 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> 调用它的任何方法上都有一个隐式的 LinkDemand。 此 LinkDemand 要求调用代码是关键安全的。 标记将 SuppressUnmanagedCodeSecurity 与特性结合使用的方法， <xref:System.Security.SecurityCriticalAttribute> 使此要求对于方法的调用方更为明显。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请使用特性标记方法或类型 <xref:System.Security.SecurityCriticalAttribute> 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Security.CA2145.TransparentMethodsShouldNotUseSuppressUnmanagedCodeSecurity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2145.transparentmethodsshouldnotusesuppressunmanagedcodesecurity/cs/ca2145.cs#1)]

### <a name="comments"></a>注释
