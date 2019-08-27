---
title: CA2114:方法安全性应是类型的超集 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: b1a360ee4ad35fd48a46f6d866912a05a584a54c
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687319"
---
# <a name="ca2114-method-security-should-be-a-superset-of-type"></a>CA2114:方法安全性应是类型安全性的超集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MethodSecurityShouldBeASupersetOfType|
|CheckId|CA2114|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 一种类型具有声明性安全，并且某一方法具有相同的安全操作中，声明性安全和安全操作不是[链接需求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)或[继承需求](https://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9)，和权限检查的类型不是该方法检查的权限的子集。

## <a name="rule-description"></a>规则说明
 同时相同的操作方法级别和类型级别的声明性安全，不应具有一种方法。 不会合并两个检查;仅方法级别要求应用。 例如，如果一个类型要求的权限`X`，并且其方法之一将请求权限`Y`，代码不需要具有权限`X`来执行此方法。

## <a name="how-to-fix-violations"></a>如何解决冲突
 检查代码，请确保这两种操作所需。 如果这两种操作是必需的请确保方法级别的操作包括在类型级别上指定的安全性。 例如，如果类型要求权限`X`，而它的方法必须要求权限`Y`，该方法应显式要求`X`和`Y`。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，如果该方法不需要指定类型的安全性。 但是，这不是普通的方案，可能表明需要进行仔细的设计检查。

## <a name="example"></a>示例
 以下示例使用环境的权限来演示违反此规则的危险。 在此示例中，应用程序代码之前拒绝类型所需的权限创建受保护的类型的实例。 在实际的威胁情况下，应用程序将需要另一种方法获取对象的实例。

 在以下示例中，库要求的写入权限的类型和读取权限的方法。

 [!code-csharp[FxCop.Security.MethodLevelSecurity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.MethodLevelSecurity/cs/FxCop.Security.MethodLevelSecurity.cs#1)]

## <a name="example"></a>示例
 下面的应用程序代码通过调用方法，即使它不满足类型级别的安全要求演示库的漏洞。

 [!code-csharp[FxCop.Security.TestMethodLevelSecurity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestMethodLevelSecurity/cs/FxCop.Security.TestMethodLevelSecurity.cs#1)]

 本示例生成以下输出。

 **[所有权限]个人信息：6/16/1964年 12:00:00 AM**
 **[（所要求的类型） 没有写入权限] 的个人信息：6/16/1964年 12:00:00 AM**
 **[（方法所需） 没有读取的权限] 无法访问的个人信息：请求失败。**
## <a name="see-also"></a>请参阅
 [安全编码准则](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)[继承需求](https://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9)[链接要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)[数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
