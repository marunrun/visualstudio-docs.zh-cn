---
title: CA2117:APTCA 类型应只扩展 APTCA 基类型
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2117
- AptcaTypesShouldOnlyExtendAptcaBaseTypes
helpviewer_keywords:
- AptcaTypesShouldOnlyExtendAptcaBaseTypes
- CA2117
ms.assetid: c505b586-2f1e-47cb-98ee-a5afcbeda70f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 43b294d72c8f8ec317803f2aa400e9cc50693162
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62545682"
---
# <a name="ca2117-aptca-types-should-only-extend-aptca-base-types"></a>CA2117:APTCA 类型应只扩展 APTCA 基类型

|||
|-|-|
|TypeName|AptcaTypesShouldOnlyExtendAptcaBaseTypes|
|CheckId|CA2117|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因

公共或受保护的程序集中类型<xref:System.Security.AllowPartiallyTrustedCallersAttribute?displayProperty=fullName>属性继承自不具有属性的程序集中声明的类型。

## <a name="rule-description"></a>规则说明

默认情况下，使用强名称的程序集中的公共或受保护类型隐式受[InheritanceDemand](xref:System.Security.Permissions.SecurityAction#System_Security_Permissions_SecurityAction_InheritanceDemand)的完全信任。 用强名称的程序集标记<xref:System.Security.AllowPartiallyTrustedCallersAttribute>(APTCA) 特性不具有这种保护。 该属性禁用继承要求。 公开的类型声明中没有继承要求的程序集是由不具有完全信任的类型继承。

APTCA 属性是完全受信任的程序集，并在程序集中的类型继承自的类型不允许部分受信任调用方，则可能会产生安全问题。 如果两个类型`T1`并`T2`满足以下条件，则恶意调用方可以使用类型`T1`绕过的隐式完全信任继承要求保护`T2`:

- `T1` 在完全受信任的程序集具有 APTCA 特性中声明的公共类型。

- `T1` 类型继承`T2`其程序集外部。

- `T2`程序集不具有 APTCA 特性，并且，因此，不应由部分受信任的程序集中的类型继承。

部分受信任的类型`X`可以继承自`T1`，并向它授予访问权限的继承成员中声明`T2`。 因为`T2`不具有 APTCA 属性，其直接派生类型 (`T1`) 必须满足的完全信任; 继承要求`T1`具有完全信任权限，因此满足此检查。 安全风险是因为`X`不参与满足继承要求保护`T2`来自不受信任的子类化。 出于此原因，用 APTCA 特性的类型不能扩展没有该属性的类型。

另一个安全问题和可能是一个更常见的活动，是派生的类型 (`T1`) 可以通过编程器错误公开受保护的成员需要完全信任的类型 (`T2`)。 此信息时，不受信任调用方访问应仅供完全受信任的类型的信息。

## <a name="how-to-fix-violations"></a>如何解决冲突

如果不需要 APTCA 特性的程序集中的冲突报告的类型，请将其删除。

如果 APTCA 特性是必需的添加一个针对完全信任继承要求为类型。 继承要求可防止不受信任的类型继承。

就可以通过将 APTCA 特性添加到报告的冲突的基类型的程序集修复与冲突。 请执行此操作必须首先进行严格的安全审查的程序集中的所有代码和依赖程序集的所有代码。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

若要安全地禁止显示此规则的警告，必须确保受保护的成员公开你的类型不直接或间接允许不受信任调用方访问敏感信息、 操作或可以以破坏方式使用的资源。

## <a name="example"></a>示例

以下示例使用两个程序集和测试应用程序来演示此规则检测到的安全漏洞。 第一个程序集不具有 APTCA 属性，不应由部分受信任的类型继承 (由`T2`前面讨论)。

[!code-csharp[FxCop.Security.NoAptcaInherit#1](../code-quality/codesnippet/CSharp/ca2117-aptca-types-should-only-extend-aptca-base-types_1.cs)]

第二个程序集，由表示`T1`前面讨论中是完全受信任，允许部分受信任调用方。

[!code-csharp[FxCop.Security.YesAptcaInherit#1](../code-quality/codesnippet/CSharp/ca2117-aptca-types-should-only-extend-aptca-base-types_2.cs)]

测试类型，由表示`X`在前面的讨论，是在部分受信任的程序集中。

[!code-csharp[FxCop.Security.TestAptcaInherit#1](../code-quality/codesnippet/CSharp/ca2117-aptca-types-should-only-extend-aptca-base-types_3.cs)]

该示例产生下面的输出：

```txt
Meet at the shady glen 2/22/2003 12:00:00 AM!
From Test: sunny meadow
Meet at the sunny meadow 2/22/2003 12:00:00 AM!
```

## <a name="related-rules"></a>相关的规则

[CA2116:APTCA 方法应只调用 APTCA 方法](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md)

## <a name="see-also"></a>请参阅

- [安全编码准则](/dotnet/standard/security/secure-coding-guidelines)
- [通过部分受信任的代码使用库](/dotnet/framework/misc/using-libraries-from-partially-trusted-code)
