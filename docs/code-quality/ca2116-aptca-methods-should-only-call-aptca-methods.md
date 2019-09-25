---
title: CA2116:APTCA 方法应只调用 APTCA 方法
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AptcaMethodsShouldOnlyCallAptcaMethods
- CA2116
helpviewer_keywords:
- AptcaMethodsShouldOnlyCallAptcaMethods
- CA2116
ms.assetid: 8b91637e-891f-4dde-857b-bf8012270ec4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f09817e9248fdc28f56ac0162e783bf72643ee5c
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232686"
---
# <a name="ca2116-aptca-methods-should-only-call-aptca-methods"></a>CA2116:APTCA 方法应只调用 APTCA 方法

|||
|-|-|
|TypeName|AptcaMethodsShouldOnlyCallAptcaMethods|
|CheckId|CA2116|
|类别|Microsoft.Security|
|重大更改|重大|

## <a name="cause"></a>原因

具有<xref:System.Security.AllowPartiallyTrustedCallersAttribute?displayProperty=fullName>属性的程序集中的方法在不具有属性的程序集中调用方法。

## <a name="rule-description"></a>规则说明

默认情况下，具有强名称的程序集中的公共或受保护方法会受到完全信任的[链接要求](/dotnet/framework/misc/link-demands)的保护;只有完全受信任的调用方可以访问具有强名称的程序集。 用<xref:System.Security.AllowPartiallyTrustedCallersAttribute> （APTCA）特性标记的强名称程序集不具有此保护。 特性禁用链接要求，使不具有完全信任的调用方可以访问该程序集，例如从 intranet 或 Internet 执行的代码。

当完全受信任的程序集上存在 APTCA 特性时，如果该程序集执行另一个不允许部分受信任调用方的程序集中的代码，则可能会出现安全漏洞。 如果两种`M1`方法`M2`满足以下条件，则恶意调用方可以使用方法`M1`绕过受保护`M2`的隐式完全信任链接要求：

- `M1`是在具有 APTCA 特性的完全受信任的程序集中声明的公共方法。

- `M1`调用的程序`M2`集`M1`外的方法。

- `M2`的程序集没有 APTCA 特性，因此不应由或代表部分受信任的调用方来执行。

部分受信任的`X`调用方可以`M1`调用方法`M1` ，从而`M2`导致调用。 由于`M2`没有 APTCA 特性，因此它的直接调用方（`M1`）必须满足完全信任的链接要求;`M1`具有完全信任，因此满足此检查。 安全风险是因为`X`不能满足防止`M2`不受信任的调用方的链接需求。 因此，具有 APTCA 特性的方法不能调用没有特性的方法。

## <a name="how-to-fix-violations"></a>如何解决冲突
如果 APCTA 属性是必需的，请使用要求来保护调用到完全信任程序集的方法。 所需的确切权限将取决于方法公开的功能。 如果可能，请使用完全信任的要求来保护方法，以确保不会向部分受信任的调用方公开基础功能。 如果无法做到这一点，请选择一组有效保护公开功能的权限。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
若要安全地禁止显示此规则发出的警告，必须确保方法公开的功能不会直接或间接地允许调用方访问可通过破坏性方式使用的敏感信息、操作或资源。

## <a name="example-1"></a>示例 1
下面的示例使用两个程序集和一个测试应用程序来说明此规则检测到的安全漏洞。 第一个程序集没有 APTCA 属性，部分受信任的调用方（ `M2`在前面的讨论中表示）不应访问该程序集。

[!code-csharp[FxCop.Security.NoAptca#1](../code-quality/codesnippet/CSharp/ca2116-aptca-methods-should-only-call-aptca-methods_1.cs)]

## <a name="example-2"></a>示例 2
第二个程序集是完全受信任的程序集，允许`M1`部分受信任的调用方（在上一讨论中表示）。

[!code-csharp[FxCop.Security.YesAptca#1](../code-quality/codesnippet/CSharp/ca2116-aptca-methods-should-only-call-aptca-methods_2.cs)]

## <a name="example-3"></a>示例 3
测试应用程序（ `X`在上一讨论中表示）是部分受信任的应用程序。

[!code-csharp[FxCop.Security.TestAptcaMethods#1](../code-quality/codesnippet/CSharp/ca2116-aptca-methods-should-only-call-aptca-methods_3.cs)]

该示例产生下面的输出：

```txt
Demand for full trust:Request failed.
ClassRequiringFullTrust.DoWork was called.
```

## <a name="related-rules"></a>相关规则

- [CA2117APTCA 类型应只扩展 APTCA 基类型](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md)

## <a name="see-also"></a>请参阅

- [安全编码准则](/dotnet/standard/security/secure-coding-guidelines)
- [通过部分受信任的代码使用库](/dotnet/framework/misc/using-libraries-from-partially-trusted-code)
- [链接需求](/dotnet/framework/misc/link-demands)
- [数据和建模](/dotnet/framework/data/index)