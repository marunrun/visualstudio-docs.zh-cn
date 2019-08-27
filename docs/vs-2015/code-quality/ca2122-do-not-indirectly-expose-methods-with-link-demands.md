---
title: CA2122:不要间接公开方法使用链接请求 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2122
- DoNotIndirectlyExposeMethodsWithLinkDemands
helpviewer_keywords:
- DoNotIndirectlyExposeMethodsWithLinkDemands
- CA2122
ms.assetid: 3eda58e7-c6ec-41c3-8112-ae0841109c6a
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: e0b173378194c099b2014093104f814f3454843d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687259"
---
# <a name="ca2122-do-not-indirectly-expose-methods-with-link-demands"></a>CA2122:不要使用链接请求间接公开方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotIndirectlyExposeMethodsWithLinkDemands|
|CheckId|CA2122|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 公共或受保护成员具有[链接要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)，并由不执行任何安全检查的成员。

## <a name="rule-description"></a>规则说明
 链接请求仅检查直接调用方的权限。 如果成员`X`使其调用方，并调用代码受链接要求，调用方没有所需的权限可以使用的安全请求`X`来访问受保护的成员。

## <a name="how-to-fix-violations"></a>如何解决冲突
 添加安全[数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)或将需求链接到该成员，以便它不再提供对受链接要求保护的成员的不安全的访问。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 若要安全地禁止显示此规则的警告，必须确保你的代码不会授予其调用方访问操作或可以以破坏方式使用的资源。

## <a name="example"></a>示例
 以下示例演示一个库，它违反了此规则和演示库的漏洞的应用程序。 示例库提供一起违反规则的两种方法。 `EnvironmentSetting`方法受链接要求无限制地访问环境变量。 `DomainInformation`方法发出安全请求其调用方的调用之前`EnvironmentSetting`。

 [!code-csharp[FxCop.Security.UnsecuredDoNotCall#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.UnsecuredDoNotCall/cs/FxCop.Security.UnsecuredDoNotCall.cs#1)]

## <a name="example"></a>示例
 下面的应用程序调用的不安全的库成员。

 [!code-csharp[FxCop.Security.TestUnsecuredDoNot1#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestUnsecuredDoNot1/cs/FxCop.Security.TestUnsecuredDoNot1.cs#1)]

 本示例生成以下输出。

 **来自未受保护成员的值： seattle.corp.contoso.com**
## <a name="see-also"></a>请参阅
 [安全编码准则](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)[链接需求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)[数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
