---
title: CA2106:保护断言
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2106
- SecureAsserts
helpviewer_keywords:
- CA2106
- SecureAsserts
ms.assetid: 91feb36e-6e2c-436c-8272-5aee31f77e98
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d4495dcbe951edd3e7eaa3b6ff0d2432bc0a7751
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232879"
---
# <a name="ca2106-secure-asserts"></a>CA2106:保护断言

|||
|-|-|
|TypeName|SecureAsserts|
|CheckId|CA2106|
|类别|Microsoft.Security|
|重大更改|重大|

## <a name="cause"></a>原因
方法断言权限，但不对调用方执行任何安全检查。

## <a name="rule-description"></a>规则说明
如果在不执行任何安全检查的情况下断言安全权限，则会在代码中留下可利用的安全漏洞。 安全堆栈审核在断言安全权限时停止。 如果在不对调用方执行任何检查的情况下断言权限，调用方可以使用您的权限间接执行代码。 如果你确定不能以有害方式使用断言，则不允许使用不带安全检查的断言。 如果调用的代码不无害，或用户无法将任意信息传递给所调用的代码，则断言不会造成危害。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请将安全要求添加到方法或其声明类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
仅在仔细检查安全检查后，禁止显示此规则发出的警告。

## <a name="see-also"></a>请参阅

- <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName>
- [安全编码准则](/dotnet/standard/security/secure-coding-guidelines)