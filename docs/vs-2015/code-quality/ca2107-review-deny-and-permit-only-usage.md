---
title: CA2107：查看 deny 和仅允许使用 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2107
- ReviewDenyAndPermitOnlyUsage
helpviewer_keywords:
- ReviewDenyAndPermitOnlyUsage
- CA2107
ms.assetid: 366f4a56-ae93-4882-81d0-bd0a55ebbc26
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 7f273ea5f58babf7a0c04f6b0758732d43aab7db
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547766"
---
# <a name="ca2107-review-deny-and-permit-only-usage"></a>CA2107:检查 deny 权限和 permit only 权限的使用情况
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|ReviewDenyAndPermitOnlyUsage|
|CheckId|CA2107|
|Category|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 方法包含指定 PermitOnly 或 Deny 安全操作的安全检查。

## <a name="rule-description"></a>规则描述
 [使用 PermitOnly 方法](https://msdn.microsoft.com/8c7bdb7f-882f-45b7-908c-6cbaa1767649)和 <xref:System.Security.CodeAccessPermission.Deny%2A?displayProperty=fullName> 安全操作的只应由具有高级安全知识的人员使用 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。 应当对使用这些安全操作的代码进行安全检查。

 Deny 改变出现的堆栈审核的默认行为，以响应安全要求。 它使你能够指定在拒绝方法的持续时间内不得授予的权限，而不考虑调用堆栈中调用方的实际权限。 如果堆栈审核检测到受 Deny 保护的方法，并且所请求的权限包含在拒绝的权限中，堆栈审核会失败。 PermitOnly 还会改变堆栈审核的默认行为。 它允许代码仅指定可授予的权限，而与调用方的权限无关。 如果堆栈审核检测到由 PermitOnly 保护的方法，并且在 PermitOnly 指定的权限中未包含请求的权限，则堆栈审核会失败。

 应认真评估依赖于这些操作的代码是否存在安全漏洞，因为它们的有用性和微妙行为有限。 请考虑下列各项：

- 拒绝或 PermitOnly 不会影响[链接需求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)。

- 如果拒绝或 PermitOnly 与引起堆栈审核的需求出现在同一堆栈帧中，则安全操作不起作用。

- 通常可以通过多种方式指定用于构造基于路径的权限的值。 拒绝访问一种形式的路径不会拒绝对所有窗体的访问。 例如，如果将文件共享 \\ \Server\Share 映射到网络驱动器 X：，则若要拒绝对共享上的文件的访问，必须拒绝 \\ \Server\Share\File、X:\File 以及访问该文件的每个其他路径。

- <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName>可以在达到 Deny 或 PermitOnly 之前终止堆栈遍历。

- 如果拒绝有任何影响，即，当调用方具有拒绝阻止的权限时，调用方可以直接访问受保护的资源，绕过拒绝。 同样，如果调用方不具有拒绝的权限，堆栈审核将失败，且不会出现 Deny。

## <a name="how-to-fix-violations"></a>如何解决冲突
 任何使用这些安全操作都会导致冲突。 若要解决冲突，请不要使用这些安全操作。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 仅在完成安全检查后，禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示 Deny 的一些限制。

 以下库包含一个类，该类具有两个完全相同的方法，但保护它们的安全请求除外。

 [!code-csharp[FxCop.Security.PermitAndDeny#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PermitAndDeny/cs/FxCop.Security.PermitAndDeny.cs#1)]

## <a name="example"></a>示例
 下面的应用程序演示 Deny 对库中的安全方法的影响。

 [!code-csharp[FxCop.Security.TestPermitAndDeny#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestPermitAndDeny/cs/FxCop.Security.TestPermitAndDeny.cs#1)]

 本示例生成以下输出。

 **需求：调用方的 Deny 对具有断言权限的需求不起作用。** 
**Linkdemand：调用方的 Deny 对具有断言权限的 LinkDemand 不起作用。** 
**Linkdemand：调用方的 Deny 对于受 LinkDemand 保护的代码不起作用。** 
**Linkdemand：此拒绝对受 LinkDemand 保护的代码不起作用。**
## <a name="see-also"></a>另请参阅
 <xref:System.Security.CodeAccessPermission.PermitOnly%2A?displayProperty=fullName> <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName>
 <xref:System.Security.CodeAccessPermission.Deny%2A?displayProperty=fullName>
 <xref:System.Security.IStackWalk.PermitOnly%2A?displayProperty=fullName>
 [安全编码准则](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)[使用 PermitOnly 方法](https://msdn.microsoft.com/8c7bdb7f-882f-45b7-908c-6cbaa1767649)[覆盖安全检查](https://msdn.microsoft.com/4acdeff5-fc05-41bf-8505-7387cdbfca28)
