---
title: CA2116:APTCA 方法应只调用 APTCA 方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AptcaMethodsShouldOnlyCallAptcaMethods
- CA2116
helpviewer_keywords:
- AptcaMethodsShouldOnlyCallAptcaMethods
- CA2116
ms.assetid: 8b91637e-891f-4dde-857b-bf8012270ec4
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c9de5178b585275ef410ad3179ba320b663536bf
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658684"
---
# <a name="ca2116-aptca-methods-should-only-call-aptca-methods"></a>CA2116:APTCA 方法应只调用 APTCA 方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AptcaMethodsShouldOnlyCallAptcaMethods|
|CheckId|CA2116|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 具有 <xref:System.Security.AllowPartiallyTrustedCallersAttribute?displayProperty=fullName> 特性的程序集中的方法在不具有属性的程序集中调用方法。

## <a name="rule-description"></a>规则说明
 默认情况下，具有强名称的程序集中的公共或受保护方法会受到完全信任的[链接要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)的保护;只有完全受信任的调用方可以访问具有强名称的程序集。 用 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> （APTCA）特性标记的强名称程序集不具有此保护。 特性禁用链接要求，使不具有完全信任的调用方可以访问该程序集，例如从 intranet 或 Internet 执行的代码。

 当完全受信任的程序集上存在 APTCA 特性时，如果该程序集执行另一个不允许部分受信任调用方的程序集中的代码，则可能会出现安全漏洞。 如果两个方法 `M1`，`M2` 满足以下条件，则恶意调用方可以使用方法 `M1` 来绕过保护 `M2` 的隐式完全信任链接要求：

- `M1` 是在具有 APTCA 特性的完全受信任的程序集中声明的公共方法。

- `M1` `M2` `M1` 的程序集外调用方法。

- `M2` 的程序集没有 APTCA 特性，因此不应由或代表部分受信任的调用方来执行。

  部分受信任的调用方 `X` 可以调用方法 `M1`，导致 `M1` 调用 `M2`。 因为 `M2` 没有 APTCA 特性，所以它的直接调用方（`M1`）必须满足完全信任的链接要求;`M1` 具有完全信任，因此满足此项检查。 安全风险是因为 `X` 不参与满足防止不受信任的调用方 `M2` 的链接需求。 因此，具有 APTCA 特性的方法不能调用没有特性的方法。

## <a name="how-to-fix-violations"></a>如何解决冲突
 如果 APCTA 属性是必需的，请使用要求来保护调用到完全信任程序集的方法。 所需的确切权限将取决于方法公开的功能。 如果可能，请使用完全信任的要求来保护方法，以确保不会向部分受信任的调用方公开基础功能。 如果无法做到这一点，请选择一组有效保护公开功能的权限。 有关要求的详细信息，请参阅[需求](https://msdn.microsoft.com/e5283e28-2366-4519-b27d-ef5c1ddc1f48)。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 若要安全地禁止显示此规则发出的警告，必须确保方法公开的功能不会直接或间接地允许调用方访问可通过破坏性方式使用的敏感信息、操作或资源。

## <a name="example"></a>示例
 下面的示例使用两个程序集和一个测试应用程序来说明此规则检测到的安全漏洞。 第一个程序集没有 APTCA 特性，部分受信任的调用方（在上一讨论中由 `M2` 表示）不应访问。

 [!code-csharp[FxCop.Security.NoAptca#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.NoAptca/cs/FxCop.Security.NoAptca.cs#1)]

## <a name="example"></a>示例
 第二个程序集是完全受信任的程序集，允许部分受信任的调用方（在上一讨论中由 `M1` 表示）。

 [!code-csharp[FxCop.Security.YesAptca#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.YesAptca/cs/FxCop.Security.YesAptca.cs#1)]

## <a name="example"></a>示例
 测试应用程序（由前面讨论的 `X` 表示）是部分受信任的应用程序。

 [!code-csharp[FxCop.Security.TestAptcaMethods#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestAptcaMethods/cs/FxCop.Security.TestAptcaMethods.cs#1)]

 本示例生成以下输出。

 **完全信任的需求：请求失败。** **已调用 
 ClassRequiringFullTrust. DoWork** 。
## <a name="related-rules"></a>相关规则
 [CA2117：APTCA 类型应只扩展 APTCA 基类型 ](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md)

## <a name="see-also"></a>请参阅
 [安全编码准则](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177) [.NET Framework 由部分受信任的代码](https://msdn.microsoft.com/a417fcd4-d3ca-4884-a308-3a1a080eac8d) [使用库从部分受信任 的代码](https://msdn.microsoft.com/library/dd66cd4c-b087-415f-9c3e-94e3a1835f74) [需求](https://msdn.microsoft.com/e5283e28-2366-4519-b27d-ef5c1ddc1f48) [链接需求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d) [数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
