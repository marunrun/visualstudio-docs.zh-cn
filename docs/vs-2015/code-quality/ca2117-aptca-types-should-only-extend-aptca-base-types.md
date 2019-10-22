---
title: CA2117： APTCA 类型应只扩展 APTCA 基类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2117
- AptcaTypesShouldOnlyExtendAptcaBaseTypes
helpviewer_keywords:
- AptcaTypesShouldOnlyExtendAptcaBaseTypes
- CA2117
ms.assetid: c505b586-2f1e-47cb-98ee-a5afcbeda70f
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 09fa055fbf1b11e06b1dde32df5a316a3ec39848
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658660"
---
# <a name="ca2117-aptca-types-should-only-extend-aptca-base-types"></a>CA2117：APTCA 类型应只扩展 APTCA 基类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AptcaTypesShouldOnlyExtendAptcaBaseTypes|
|CheckId|CA2117|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 具有 <xref:System.Security.AllowPartiallyTrustedCallersAttribute?displayProperty=fullName> 特性的程序集中的公共或受保护类型从不具有属性的程序集中声明的类型继承。

## <a name="rule-description"></a>规则说明
 默认情况下，具有强名称的程序集中的公共或受保护类型由完全信任的[继承要求](https://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9)隐式保护。 用 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> （APTCA）特性标记的具有强名称的程序集不具有此保护。 特性禁用继承要求。 这使得在程序集中声明的公开类型可由不具有完全信任的类型继承。

 当完全受信任的程序集上存在 APTCA 特性，并且程序集中的类型从不允许部分受信任调用方的类型继承时，可能会出现安全漏洞。 如果两种类型 `T1` 和 `T2` 满足以下条件，则恶意调用方可以使用类型 `T1` 来绕过保护 `T2` 的隐式完全信任继承要求：

- `T1` 是在具有 APTCA 特性的完全受信任的程序集中声明的公共类型。

- `T1` 继承自其程序集外部 `T2` 类型。

- `T2` 的程序集没有 APTCA 特性，因此不应由部分受信任的程序集中的类型继承。

  部分受信任的类型 `X` 可继承自 `T1`，这使其可以访问 `T2` 中声明的继承成员。 由于 `T2` 没有 APTCA 特性，因此它的直接派生类型（`T1`）必须满足完全信任的继承要求; `T1` 具有完全信任，因此满足此检查。 安全风险是因为 `X` 不参与满足防止不受信任的子类中 `T2` 的继承要求。 出于此原因，具有 APTCA 特性的类型不能扩展没有特性的类型。

  另一个安全问题（可能更常见）是派生类型（`T1`）可以通过程序员错误，从要求完全信任的类型（`T2`）公开受保护的成员。 发生这种情况时，不受信任的调用方可以访问只应提供给完全受信任的类型的信息。

## <a name="how-to-fix-violations"></a>如何解决冲突
 如果冲突报告的类型位于不需要 APTCA 属性的程序集中，请将其删除。

 如果 APTCA 特性是必需的，则为该类型添加完全信任的继承要求。 这可以防止不受信任的类型继承。

 可以通过将 APTCA 特性添加到冲突报告的基类型的程序集来修复冲突。 如果没有先对程序集中的所有代码和依赖程序集的所有代码进行大量的安全检查，请不要执行此操作。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 若要安全地禁止显示此规则发出的警告，您必须确保您的类型公开的受保护成员不直接或间接允许不受信任的调用方访问可通过破坏性方式使用的敏感信息、操作或资源。

## <a name="example"></a>示例
 下面的示例使用两个程序集和一个测试应用程序来说明此规则检测到的安全漏洞。 第一个程序集没有 APTCA 特性，不应由部分受信任的类型继承（由前面讨论中的 `T2` 表示）。

 [!code-csharp[FxCop.Security.NoAptcaInherit#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.NoAptcaInherit/cs/FxCop.Security.NoAptcaInherit.cs#1)]

## <a name="example"></a>示例
 第二个程序集（由上一讨论中的 `T1` 表示）是完全受信任的，允许部分受信任的调用方。

 [!code-csharp[FxCop.Security.YesAptcaInherit#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.YesAptcaInherit/cs/FxCop.Security.YesAptcaInherit.cs#1)]

## <a name="example"></a>示例
 由前面讨论 `X` 表示的测试类型位于部分受信任的程序集中。

 [!code-csharp[FxCop.Security.TestAptcaInherit#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestAptcaInherit/cs/FxCop.Security.TestAptcaInherit.cs#1)]

 本示例生成以下输出。

 **在偷偷 glen 2/22/2003 12:00:00 AM！** 
**测试： sunny meadow** 
**在 SUNNY meadow 2/22/2003 12:00:00 AM！**
## <a name="related-rules"></a>相关规则
 [CA2116：APTCA 方法应只调用 APTCA 方法](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md)

## <a name="see-also"></a>请参阅
 [安全编码准则](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177) [.NET Framework 由部分受信任代码使用的程序集通过](https://msdn.microsoft.com/a417fcd4-d3ca-4884-a308-3a1a080eac8d)[部分受信任的代码](https://msdn.microsoft.com/library/dd66cd4c-b087-415f-9c3e-94e3a1835f74)[继承请求](https://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9)来调用的程序集
