---
title: CA2107:检查 deny 权限和 permit only 权限的使用情况
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2107
- ReviewDenyAndPermitOnlyUsage
helpviewer_keywords:
- ReviewDenyAndPermitOnlyUsage
- CA2107
ms.assetid: 366f4a56-ae93-4882-81d0-bd0a55ebbc26
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9c7f3bdc6351f30d5cad60a7ed9663824fa3d434
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66714709"
---
# <a name="ca2107-review-deny-and-permit-only-usage"></a>CA2107:检查 deny 权限和 permit only 权限的使用情况

|||
|-|-|
|TypeName|ReviewDenyAndPermitOnlyUsage|
|CheckId|CA2107|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因

方法包含指定 PermitOnly 或拒绝安全操作的安全检查。

## <a name="rule-description"></a>规则说明

<xref:System.Security.CodeAccessPermission.Deny%2A?displayProperty=fullName>安全操作应仅由具有.NET 安全性的高级的知识的用户使用。 应当对使用这些安全操作的代码进行安全检查。

拒绝更改而发生响应安全要求的堆栈审核的默认行为。 它允许你指定必须未在拒绝的方法，而不考虑调用堆栈中的调用方的实际权限的持续时间内授予的权限。 如果堆栈遍历检测到拒绝，受保护的方法，并且如果要求的权限包含在被拒绝的权限，则堆栈审核失败。 PermitOnly 也会更改堆栈遍历的默认行为。 它允许指定调用方的权限也是如此，可授予这些权限的代码。 如果堆栈遍历检测到 PermitOnly，受保护的方法和中所指定的 PermitOnly 的权限不包括所需的权限，则堆栈审核失败。

依赖于这些操作代码应认真评估存在安全漏洞，因为其用途有限和细微的行为。 考虑以下情况：

- [链接需求](/dotnet/framework/misc/link-demands)的 Deny 或 PermitOnly 不会影响。

- 如果 Deny 或 PermitOnly 发生导致堆栈遍历需求相同的堆栈帧中，安全操作将产生任何影响。

- 通常可以通过多种方法指定用于构造基于路径的权限的值。 拒绝访问路径的一个窗体不拒绝所有窗体的访问。 例如，如果文件共享\\\Server\Share 映射到网络驱动器 x:，以拒绝访问的文件共享上，则必须拒绝\\\Server\Share\File、 X:\File 和每个其他访问文件的路径。

- <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName>达到 Deny 或 PermitOnly 之前可以终止堆栈遍历。

- 如果拒绝都没有任何效果，即当调用方具有的权限被拒绝，阻止调用方可以访问受保护的资源直接，绕过拒绝。 同样，如果调用方没有被拒绝的权限，堆栈审核会失败而无需拒绝。

## <a name="how-to-fix-violations"></a>如何解决冲突

任何使用这些安全操作而导致违反了。 若要解决冲突，不要使用这些安全操作。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

只有在完成安全审查后，禁止显示此规则的警告。

## <a name="example-1"></a>示例 1

下面的示例演示了拒绝的一些限制。 库包含具有相同，仅对其进行保护的安全需求的两个方法的类。

[!code-csharp[FxCop.Security.PermitAndDeny#1](../code-quality/codesnippet/CSharp/ca2107-review-deny-and-permit-only-usage_1.cs)]

## <a name="example-2"></a>示例 2

下面的应用程序库中演示的拒绝对受保护的方法的影响。

[!code-csharp[FxCop.Security.TestPermitAndDeny#1](../code-quality/codesnippet/CSharp/ca2107-review-deny-and-permit-only-usage_2.cs)]

该示例产生下面的输出：

```txt
Demand: Caller's Deny has no effect on Demand with the asserted permission.
LinkDemand: Caller's Deny has no effect on LinkDemand with the asserted permission.
LinkDemand: Caller's Deny has no effect with LinkDemand-protected code.
LinkDemand: This Deny has no effect with LinkDemand-protected code.
```

## <a name="see-also"></a>请参阅

- <xref:System.Security.CodeAccessPermission.PermitOnly%2A?displayProperty=fullName>
- <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName>
- <xref:System.Security.CodeAccessPermission.Deny%2A?displayProperty=fullName>
- <xref:System.Security.IStackWalk.PermitOnly%2A?displayProperty=fullName>
- [安全编码准则](/dotnet/standard/security/secure-coding-guidelines)