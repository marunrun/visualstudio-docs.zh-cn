---
title: CA2122:不要使用链接请求间接公开方法
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2122
- DoNotIndirectlyExposeMethodsWithLinkDemands
helpviewer_keywords:
- DoNotIndirectlyExposeMethodsWithLinkDemands
- CA2122
ms.assetid: 3eda58e7-c6ec-41c3-8112-ae0841109c6a
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6850cee67a0dfed4b386eef5ed7cb021d3c76a4d
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232512"
---
# <a name="ca2122-do-not-indirectly-expose-methods-with-link-demands"></a>CA2122:不要使用链接请求间接公开方法

|||
|-|-|
|TypeName|DoNotIndirectlyExposeMethodsWithLinkDemands|
|CheckId|CA2122|
|类别|Microsoft.Security|
|重大更改|不间断|

## <a name="cause"></a>原因
公共或受保护成员具有[链接要求](/dotnet/framework/misc/link-demands)，且由不执行任何安全检查的成员调用。

## <a name="rule-description"></a>规则说明
链接请求仅检查直接调用方的权限。 如果成员`X`不对其调用方进行安全要求，并调用受链接要求保护的代码，则没有必要权限的调用方可以`X`使用来访问受保护的成员。

## <a name="how-to-fix-violations"></a>如何解决冲突
向成员添加安全[数据和建模](/dotnet/framework/data/index)或链接要求，使其不再提供对链接请求保护成员的安全访问。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
若要安全地禁止显示此规则发出的警告，您必须确保您的代码不会向调用方授予对可通过破坏性方式使用的操作或资源的访问权限。

## <a name="example-1"></a>示例 1
下面的示例显示了一个与该规则冲突的库，以及一个演示库的漏洞的应用程序。 示例库提供了两个共同违反规则的方法。 此`EnvironmentSetting`方法受对环境变量的无限制访问的链接要求的保护。 此`DomainInformation`方法在调用`EnvironmentSetting`之前不会对其调用方进行安全要求。

[!code-csharp[FxCop.Security.UnsecuredDoNotCall#1](../code-quality/codesnippet/CSharp/ca2122-do-not-indirectly-expose-methods-with-link-demands_1.cs)]

## <a name="example-2"></a>示例 2
以下应用程序将调用未受保护的库成员。

[!code-csharp[FxCop.Security.TestUnsecuredDoNot1#1](../code-quality/codesnippet/CSharp/ca2122-do-not-indirectly-expose-methods-with-link-demands_2.cs)]

该示例产生下面的输出：

```txt
*Value from unsecured member: seattle.corp.contoso.com
```

## <a name="see-also"></a>请参阅

- [安全编码准则](/dotnet/standard/security/secure-coding-guidelines)
- [链接需求](/dotnet/framework/misc/link-demands)
- [数据和建模](/dotnet/framework/data/index)