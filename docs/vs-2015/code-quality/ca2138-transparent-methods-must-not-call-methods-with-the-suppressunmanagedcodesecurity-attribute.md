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
ms.openlocfilehash: 65e00d319bff3bbfd3c441c6b60ed8a703e69251
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72654803"
---
# <a name="ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute"></a>CA2138：透明方法不得调用具有 SuppressUnmanagedCodeSecurity 特性的方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods|
|CheckId|CA2138|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 安全透明方法调用使用 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> 特性标记的方法。

## <a name="rule-description"></a>规则说明
 此规则对直接调用本机代码的任何透明方法（例如通过使用 P/Invoke （平台调用）调用）引发。 使用 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> 特性标记的 P/Invoke 和 COM 互操作方法将导致针对调用方法执行的 LinkDemand。 由于安全透明代码不能满足 Linkdemand，此代码也无法调用用 SuppressUnmanagedCodeSecurity 特性标记的方法，也无法调用用 SuppressUnmanagedCodeSecurity 特性标记的类的方法。 方法将失败，或者要求将转换为完全请求。

 违反此规则会导致级别2安全透明度模型中的 <xref:System.MethodAccessException>，以及对第1级透明度模型中 <xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A> 的完全要求。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请删除 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> 特性，并使用 <xref:System.Security.SecurityCriticalAttribute> 或 <xref:System.Security.SecuritySafeCriticalAttribute> 特性标记该方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 [!code-csharp[FxCop.Security.CA2138.TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2138.transparentmethodsmustnotcallsuppressunmanagedcodesecuritymethods/cs/ca2138.cs#1)]
