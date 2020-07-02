---
title: CA2122：不要通过链接请求间接公开方法 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 846ce010cddfd505bb967ec612a5c31dd8321977
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544321"
---
# <a name="ca2122-do-not-indirectly-expose-methods-with-link-demands"></a>CA2122:不要使用链接请求间接公开方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|DoNotIndirectlyExposeMethodsWithLinkDemands|
|CheckId|CA2122|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 公共或受保护成员具有[链接要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)，且由不执行任何安全检查的成员调用。

## <a name="rule-description"></a>规则描述
 链接请求仅检查直接调用方的权限。 如果成员 `X` 不对其调用方进行安全要求，并调用受链接要求保护的代码，则没有必要权限的调用方可以使用 `X` 来访问受保护的成员。

## <a name="how-to-fix-violations"></a>如何解决冲突
 向成员添加安全[数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)或链接要求，使其不再提供对链接请求保护成员的安全访问。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 若要安全地禁止显示此规则发出的警告，您必须确保您的代码不会向调用方授予对可通过破坏性方式使用的操作或资源的访问权限。

## <a name="example"></a>示例
 下面的示例显示了一个与该规则冲突的库，以及一个演示库的漏洞的应用程序。 示例库提供了两个共同违反规则的方法。 此 `EnvironmentSetting` 方法受对环境变量的无限制访问的链接要求的保护。 此 `DomainInformation` 方法在调用之前不会对其调用方进行安全要求 `EnvironmentSetting` 。

 [!code-csharp[FxCop.Security.UnsecuredDoNotCall#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.UnsecuredDoNotCall/cs/FxCop.Security.UnsecuredDoNotCall.cs#1)]

## <a name="example"></a>示例
 以下应用程序将调用未受保护的库成员。

 [!code-csharp[FxCop.Security.TestUnsecuredDoNot1#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestUnsecuredDoNot1/cs/FxCop.Security.TestUnsecuredDoNot1.cs#1)]

 本示例生成以下输出。

 **来自不安全成员的值： seattle.corp.contoso.com**
## <a name="see-also"></a>另请参阅
 [安全编码准则](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)[链接要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)[数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
