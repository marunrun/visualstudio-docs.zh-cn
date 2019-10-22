---
title: CA2143：透明方法不应使用安全要求 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2143
ms.assetid: 5d3923d7-cf40-4512-bc5c-0db0e0d6e25a
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: bcfce9a80d02e525212d3f59173df4a7e8fbe968
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662703"
---
# <a name="ca2143-transparent-methods-should-not-use-security-demands"></a>CA2143：透明方法不应使用安全要求
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|TransparentMethodsShouldNotDemand|
|CheckId|CA2143|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 透明类型或方法以声明方式标记 <xref:System.Security.Permissions.SecurityAction?displayProperty=fullName> `.Demand` 需求或方法调用 <xref:System.Security.CodeAccessPermission.Demand%2A?displayProperty=fullName> 方法。

## <a name="rule-description"></a>规则说明
 安全透明代码不应负责验证某个操作的安全，因此不应要求权限。 安全透明代码应使用完整的需求来作出安全决策并且安全关键代码不应依赖透明代码以进行完全的请求。 执行安全检查的任何代码（如安全要求）应改为安全关键。

## <a name="how-to-fix-violations"></a>如何解决冲突
 通常，若要修复与此规则的冲突，请使用 <xref:System.Security.SecuritySafeCriticalAttribute> 特性标记该方法。 你还可以删除该需求。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 规则文件位于以下代码上，因为透明方法会作出声明性安全要求。

 [!code-csharp[FxCop.Security.CA2143.TransparentMethodsShouldNotDemand#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2143.transparentmethodsshouldnotdemand/cs/ca2143 - transparentmethodsshouldnotdemand.cs#1)]

## <a name="see-also"></a>请参阅
 [CA2142：不应使用 LinkDemand 保护透明代码](../code-quality/ca2142-transparent-code-should-not-be-protected-with-linkdemands.md)
