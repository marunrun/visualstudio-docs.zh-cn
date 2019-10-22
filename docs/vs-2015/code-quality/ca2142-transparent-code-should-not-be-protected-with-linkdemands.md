---
title: CA2142：不应通过 Linkdemand 保护透明代码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2142
ms.assetid: 6dc59053-5dd9-4583-bf10-5f339107e59f
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a9d8986e9d1e6fc3f614e23fff3f6a24c1cc6e91
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72602777"
---
# <a name="ca2142-transparent-code-should-not-be-protected-with-linkdemands"></a>CA2142：不应使用 LinkDemand 保护透明代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|TransparentMethodsShouldNotBeProtectedWithLinkDemands|
|CheckId|CA2142|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 透明方法需要 <xref:System.Security.Permissions.SecurityAction> 或其他安全要求。

## <a name="rule-description"></a>规则说明
 对于需要 LinkDemand 来访问它们的透明方法，将会引发此规则。 安全透明代码不应负责验证某个操作的安全，因此不应要求权限。 因为透明方法应为安全特定方法，所以它们不应进行任何安全决策。 此外，保证安全决策的安全关键代码不应依赖透明代码来进行此类决定。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请删除对透明方法的链接请求，或在执行安全检查（如安全要求）时使用 <xref:System.Security.SecuritySafeCriticalAttribute> 特性标记该方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 在下面的示例中，由于方法是透明的，并使用包含 <xref:System.Security.Permissions.SecurityAction> 的 LinkDemand <xref:System.Security.PermissionSet> 进行标记，因此该方法将在方法上激发。

 [!code-csharp[FxCop.Security.CA2142.TransparentMethodsShouldNotBeProtectedWithLinkDemands#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2142.transparentmethodsshouldnotbeprotectedwithlinkdemands/cs/ca2142 -transparentmethodsshouldnotbeprotectedwithlinkdemands.cs#1)]

 不禁止显示此规则发出的警告。
