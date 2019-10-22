---
title: CA2135：级别2程序集不应包含 Linkdemand |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2135
ms.assetid: 7a775285-42d2-4f13-8434-3fdb0deeebe6
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1248ac41a757ba2fc26ef0659c0f93ee325bc605
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72602949"
---
# <a name="ca2135-level-2-assemblies-should-not-contain-linkdemands"></a>CA2135：级别 2 程序集不应包含 LinkDemand
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|SecurityRuleSetLevel2MethodsShouldNotBeProtectedWithLinkDemands|
|CheckId|CA2135|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 类或类成员正在使用级别2安全的应用程序中的 <xref:System.Security.Permissions.SecurityAction>。

## <a name="rule-description"></a>规则说明
 在级别为 2 的安全规则集中已弃用 LinkDemand。 使用 <xref:System.Security.SecurityCriticalAttribute> 特性标记方法、类型和字段，而不是使用 Linkdemand 在实时（JIT）编译时强制安全性。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请删除 <xref:System.Security.Permissions.SecurityAction>，并使用 <xref:System.Security.SecurityCriticalAttribute> 特性标记该类型或成员。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 在下面的示例中，应删除 <xref:System.Security.Permissions.SecurityAction>，并以 <xref:System.Security.SecurityCriticalAttribute> 特性标记方法。

 [!code-csharp[FxCop.Security.CA2135.SecurityRuleSetLevel2MethodsShouldNotBeProtectedWithLinkDemands#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2135.securityrulesetlevel2methodsshouldnotbeprotectedwithlinkdemands/cs/ca2135.cs#1)]
