---
title: CA2138：透明方法不得调用具有 SuppressUnmanagedCodeSecurity 特性的方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2138
ms.assetid: a14c4d32-f079-4f3a-956c-a1657cde0f66
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 35cc152998b15a2fd4c4ff02e4730cdfae5366cb
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546492"
---
# <a name="ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute"></a>CA2138:透明方法不得调用具有 SuppressUnmanagedCodeSecurity 特性的方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods|
|CheckId|CA2138|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 安全透明方法调用使用特性标记的方法 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> 。

## <a name="rule-description"></a>规则描述
 此规则对直接调用本机代码的任何透明方法（例如通过使用 P/Invoke （平台调用）调用）引发。 使用特性标记的 P/Invoke 和 COM 互操作方法将 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> 导致针对调用方法执行的 LinkDemand。 由于安全透明代码不能满足 Linkdemand，此代码也无法调用用 SuppressUnmanagedCodeSecurity 特性标记的方法，也无法调用用 SuppressUnmanagedCodeSecurity 特性标记的类的方法。 方法将失败，或者要求将转换为完全请求。

 违反此规则会导致 <xref:System.MethodAccessException> 在级别2安全透明度模型中出现，并 <xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A> 在1级透明度模型中提供完全要求。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请删除 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> 特性，并使用或特性标记该方法 <xref:System.Security.SecurityCriticalAttribute> <xref:System.Security.SecuritySafeCriticalAttribute> 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 [!code-csharp[FxCop.Security.CA2138.TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2138.transparentmethodsmustnotcallsuppressunmanagedcodesecuritymethods/cs/ca2138.cs#1)]
