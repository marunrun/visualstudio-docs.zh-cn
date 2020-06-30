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
ms.openlocfilehash: cbb68855832e84150b81c8a8a6fde47bf9433edc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547701"
---
# <a name="ca2135-level-2-assemblies-should-not-contain-linkdemands"></a>CA2135:级别 2 程序集不应包含 LinkDemand
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|SecurityRuleSetLevel2MethodsShouldNotBeProtectedWithLinkDemands|
|CheckId|CA2135|
|Category|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 类或类成员正在 <xref:System.Security.Permissions.SecurityAction> 使用级别2安全的应用程序中使用。

## <a name="rule-description"></a>规则描述
 在级别为 2 的安全规则集中已弃用 LinkDemand。 使用特性标记方法、类型和字段，而不是使用 Linkdemand 在实时（JIT）编译时强制安全性 <xref:System.Security.SecurityCriticalAttribute> 。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请删除 <xref:System.Security.Permissions.SecurityAction> 并使用特性标记类型或成员 <xref:System.Security.SecurityCriticalAttribute> 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 在下面的示例中， <xref:System.Security.Permissions.SecurityAction> 应删除，并将方法标记为 <xref:System.Security.SecurityCriticalAttribute> 属性。

 [!code-csharp[FxCop.Security.CA2135.SecurityRuleSetLevel2MethodsShouldNotBeProtectedWithLinkDemands#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2135.securityrulesetlevel2methodsshouldnotbeprotectedwithlinkdemands/cs/ca2135.cs#1)]
