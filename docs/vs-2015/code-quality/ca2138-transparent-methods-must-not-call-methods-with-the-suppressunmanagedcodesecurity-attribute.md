---
title: CA2138:透明方法不得调用具有 SuppressUnmanagedCodeSecurity 特性的方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2138
ms.assetid: a14c4d32-f079-4f3a-956c-a1657cde0f66
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 4e9a9e10f928efe6bcff6fb3d49c1b1cd7b1bd1c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154294"
---
# <a name="ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute"></a>CA2138:透明方法不得调用具有 SuppressUnmanagedCodeSecurity 特性的方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods|
|CheckId|CA2138|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 安全透明方法调用的方法将标有<xref:System.Security.SuppressUnmanagedCodeSecurityAttribute>属性。

## <a name="rule-description"></a>规则说明
 直接调用到本机代码，例如，通过使用任何透明方法将触发此规则通过 P/Invoke (平台 invoke) 调用。 P/Invoke 和 COM 互操作方法标记有<xref:System.Security.SuppressUnmanagedCodeSecurityAttribute>属性结果在完成针对调用方法的 LinkDemand。 由于安全透明代码无法满足 LinkDemands，代码也不能调用具有 SuppressUnmanagedCodeSecurity 特性标记的方法或具有 SuppressUnmanagedCodeSecurity 特性标记的类的方法。 该方法将失败，或需将转换为的完全要求。

 违反此规则会导致<xref:System.MethodAccessException>中的第 2 级安全性透明模型，以及为的完全要求<xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A>级别 1 透明度模型中。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请删除<xref:System.Security.SuppressUnmanagedCodeSecurityAttribute>属性，此方法标记<xref:System.Security.SecurityCriticalAttribute>或<xref:System.Security.SecuritySafeCriticalAttribute>属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 [!code-csharp[FxCop.Security.CA2138.TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2138.transparentmethodsmustnotcallsuppressunmanagedcodesecuritymethods/cs/ca2138.cs#1)]
