---
title: CA2135:级别 2 程序集不应包含 LinkDemand
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2135
ms.assetid: 7a775285-42d2-4f13-8434-3fdb0deeebe6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d466a508eade835563627a829f937416a24972a0
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920637"
---
# <a name="ca2135-level-2-assemblies-should-not-contain-linkdemands"></a>CA2135:级别 2 程序集不应包含 LinkDemand

|||
|-|-|
|TypeName|SecurityRuleSetLevel2MethodsShouldNotBeProtectedWithLinkDemands|
|CheckId|CA2135|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
类或类成员正在使用级别 2 <xref:System.Security.Permissions.SecurityAction>安全的应用程序中使用。

## <a name="rule-description"></a>规则说明
在级别为 2 的安全规则集中已弃用 LinkDemand。 使用<xref:System.Security.SecurityCriticalAttribute>特性标记方法、类型和字段, 而不是使用 linkdemand 在实时 (JIT) 编译时强制安全性。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复<xref:System.Security.SecurityCriticalAttribute>与此规则的冲突, 请<xref:System.Security.Permissions.SecurityAction>删除并使用特性标记类型或成员。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
在下面的示例中, <xref:System.Security.Permissions.SecurityAction>应删除, 并将方法标记<xref:System.Security.SecurityCriticalAttribute>为属性。

[!code-csharp[FxCop.Security.CA2135.SecurityRuleSetLevel2MethodsShouldNotBeProtectedWithLinkDemands#1](../code-quality/codesnippet/CSharp/ca2135-level-2-assemblies-should-not-contain-linkdemands_1.cs)]