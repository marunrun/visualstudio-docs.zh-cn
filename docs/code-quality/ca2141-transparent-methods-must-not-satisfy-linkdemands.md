---
title: CA2141：透明方法不得满足 LinkDemand
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2141
ms.assetid: 2957f5f7-c511-4180-ba80-752034f10a77
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0365d82917b8cfbaf291d557a6ac2d95c220562a
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232119"
---
# <a name="ca2141transparent-methods-must-not-satisfy-linkdemands"></a>CA2141：透明方法不得满足 LinkDemand

|||
|-|-|
|TypeName|TransparentMethodsMustNotSatisfyLinkDemands|
|CheckId|CA2141|
|类别|Microsoft.Security|
|重大更改|重大|

## <a name="cause"></a>原因
安全透明方法调用未用<xref:System.Security.AllowPartiallyTrustedCallersAttribute> （APTCA）特性标记的程序集中的方法，或者安全透明方法满足某个类型或方法的。 <xref:System.Security.Permissions.SecurityAction> `.LinkDemand`

## <a name="rule-description"></a>规则说明
满足 LinkDemand 是一种安全敏感的操作，可能会导致意外的权限提升。 安全透明代码不得满足 Linkdemand，因为它不受与安全关键代码相同的安全审核要求。 安全规则集1级程序集中的透明方法会导致在运行时将其满足的所有 Linkdemand 转换为完全需求，这可能会导致性能问题。 在安全规则集级别2程序集中，如果透明方法尝试满足 LinkDemand，则它们将无法在实时（JIT）编译器中进行编译。

在使用级别2安全性的程序集中，通过安全透明方法尝试实现 linkdemand，或在非 APTCA 程序集中调用方法会引发<xref:System.MethodAccessException>; 在第1级程序集中，LinkDemand 成为完全要求。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请使用<xref:System.Security.SecurityCriticalAttribute>或<xref:System.Security.SecuritySafeCriticalAttribute>特性标记访问方法，或从访问的方法中删除该 LinkDemand。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
在此示例中，透明方法尝试调用具有 LinkDemand 的方法。 此规则将在此代码上触发。

[!code-csharp[FxCop.Security.CA2141.TransparentMethodsMustNotSatisfyLinkDemands#1](../code-quality/codesnippet/CSharp/ca2141-transparent-methods-must-not-satisfy-linkdemands_1.cs)]