---
title: CA2149：透明方法不得调入本机代码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2149
ms.assetid: 28951bd7-f3db-4871-99aa-bad68d1ead80
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5c1e254ae7912efbb6773155ed834e54a1db1832
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546323"
---
# <a name="ca2149-transparent-methods-must-not-call-into-native-code"></a>CA2149:透明方法不得调入本机代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|TransparentMethodsMustNotCallNativeCode|
|CheckId|CA2149|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 方法通过方法存根（如 P/Invoke）调用本机函数。

## <a name="rule-description"></a>规则描述
 对于直接调用到本机代码中（例如通过使用 P/Invoke）的任何透明方法，将引发此规则。 违反此规则会导致 <xref:System.MethodAccessException> 级别2透明度模型中出现，并 <xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A> 在1级透明度模型中提供完全要求。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请使用或特性标记调用本机代码的 <xref:System.Security.SecurityCriticalAttribute> 方法 <xref:System.Security.SecuritySafeCriticalAttribute> 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 [!code-csharp[FxCop.Security.CA2149.TransparentMethodsMustNotCallNativeCode#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2149.transparentmethodsmustnotcallnativecode/cs/ca2149 - transparentmethodsmustnotcallnativecode.cs#1)]
