---
title: CA2114：方法安全应为类型 | 的超集Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MethodSecurityShouldBeASupersetOfType
- CA2114
helpviewer_keywords:
- CA2114
- MethodSecurityShouldBeASupersetOfType
ms.assetid: 663f7aa4-8be5-4bd5-be92-4e9444f07077
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d7879d8b2aa9eb4ece1ce07f89681b6c0b0f5f31
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534701"
---
# <a name="ca2114-method-security-should-be-a-superset-of-type"></a>CA2114:方法安全性应是类型安全性的超集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|MethodSecurityShouldBeASupersetOfType|
|CheckId|CA2114|
|Category|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 类型具有声明性安全，其中一种方法为同一安全操作提供声明性安全，并且安全操作不是[链接要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)或[继承要求](https://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9)，且由该类型检查的权限不是方法所检查的权限的子集。

## <a name="rule-description"></a>规则描述
 一个方法不应同时具有相同操作的方法级别和类型级别的声明性安全。 这两个检查不组合在一起;仅应用方法级需求。 例如，如果某一类型要求权限 `X` ，并且它的某个方法要求权限 `Y` ，则代码不需要具有 `X` 执行方法的权限。

## <a name="how-to-fix-violations"></a>如何解决冲突
 检查代码以确保这两个操作都是必需的。 如果这两个操作都是必需的，请确保方法级别的操作包括在类型级别指定的安全性。 例如，如果你的类型需要权限 `X` ，并且其方法还必须需要权限 `Y` ，则该方法应显式需要 `X` 和 `Y` 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果方法不需要类型指定的安全性，则可以安全地禁止显示此规则发出的警告。 但这并不是一个普通方案，可能表明需要仔细设计评审。

## <a name="example"></a>示例
 下面的示例使用环境权限来演示违反此规则的危险。 在此示例中，应用程序代码在拒绝类型所需的权限之前创建了受保护类型的实例。 在实际威胁方案中，应用程序需要另一种方法来获取对象的实例。

 在下面的示例中，库请求类型的写入权限和对方法的读取权限。

 [!code-csharp[FxCop.Security.MethodLevelSecurity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.MethodLevelSecurity/cs/FxCop.Security.MethodLevelSecurity.cs#1)]

## <a name="example"></a>示例
 以下应用程序代码通过调用方法来演示库的漏洞，即使它不符合类型级安全要求。

 [!code-csharp[FxCop.Security.TestMethodLevelSecurity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestMethodLevelSecurity/cs/FxCop.Security.TestMethodLevelSecurity.cs#1)]

 本示例生成以下输出。

 **[所有权限] 个人信息：上午 6/16/1964 12:00:00** 
 **[没有写入权限（要求类型）] 个人信息： 6/16/1964 12:00:00 AM** 
 **[没有读取权限（方法要求）] 无法访问个人信息：请求失败。**
## <a name="see-also"></a>另请参阅
 [安全编码准则](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)[继承要求](https://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9)[链接需求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)[数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
