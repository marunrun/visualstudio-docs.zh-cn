---
title: CA2147:透明方法不得使用安全断言
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SecurityTransparentCodeShouldNotAssert
- CA2147
- CA2128
helpviewer_keywords:
- CA2128
- SecurityTransparentCodeShouldNotAssert
ms.assetid: 5d31e940-e599-4b23-9b28-1c336f8d910e
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e1b56001f5a083317911edde9282b66758deb1b6
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920716"
---
# <a name="ca2147-transparent-methods-may-not-use-security-asserts"></a>CA2147:透明方法不得使用安全断言

|||
|-|-|
|TypeName|SecurityTransparentCodeShouldNotAssert|
|CheckId|CA2147|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
被标记为<xref:System.Security.SecurityTransparentAttribute>的代码未被授予足够的权限进行断言。

## <a name="rule-description"></a>规则说明
此规则分析程序集中的所有方法和类型, 该程序集为 100% 透明或混合透明/关键, 并标志的<xref:System.Security.CodeAccessPermission.Assert%2A>任何声明性或命令性用法。

在运行时, 对从透明<xref:System.Security.CodeAccessPermission.Assert%2A>代码进行的任何调用都<xref:System.InvalidOperationException>将导致引发。 这种情况可能发生在 100% 透明程序集, 也可能出现在混合透明/关键程序集中, 其中方法或类型声明为透明, 但包含声明性或命令式断言。

.NET Framework 2.0 引入了一个名为 "*透明度*" 的特性。 各个方法、字段、接口、类和类型可以是透明的或关键的。

不允许透明代码提升安全权限。 因此, 任何授予或要求的权限都将自动通过代码传递给调用方或主机应用程序域。 提升的示例包括断言、linkdemand、SuppressUnmanagedCode 和`unsafe`代码。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要解决此问题, 请将调用断言<xref:System.Security.SecurityCriticalAttribute>的代码标记为, 或删除断言。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
请勿禁止显示此规则的消息。

## <a name="example"></a>示例
如果`SecurityTestClass`是透明的, 则`Assert`当该方法引发<xref:System.InvalidOperationException>时, 此代码将失败。

[!code-csharp[FxCop.Security.CA2147.TransparentMethodsMustNotUseSecurityAsserts#1](../code-quality/codesnippet/CSharp/ca2147-transparent-methods-may-not-use-security-asserts_1.cs)]

## <a name="example"></a>示例
其中一种方法是在下面的示例中查看 SecurityTransparentMethod 方法, 如果该方法被认为是安全的, 则将 SecurityTransparentMethod 标记为安全关键。 这要求在方法上执行详细的、完整和无错误的安全审核, 以及在断言下的方法中发生的任何调用:

[!code-csharp[FxCop.Security.SecurityTransparentCode2#1](../code-quality/codesnippet/CSharp/ca2147-transparent-methods-may-not-use-security-asserts_2.cs)]

另一种方法是从代码中删除断言, 并让任何后续的文件 i/o 权限要求在 SecurityTransparentMethod 到调用方之前流动。 这将启用安全检查。 在这种情况下, 不需要安全审核, 因为权限要求将流向调用方和/或应用程序域。 权限要求通过安全策略、宿主环境和代码源权限授予进行严格控制。

## <a name="see-also"></a>请参阅
[安全警告](../code-quality/security-warnings.md)