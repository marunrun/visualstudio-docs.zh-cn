---
title: CA2132：默认构造函数必须至少与基类型默认构造函数相同 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2132
ms.assetid: e758afa1-8bde-442a-8a0a-bd1ea7b0ce4d
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0ae271b116b372d4ae732d97ff3f9651ff9db426
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72643296"
---
# <a name="ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors"></a>CA2132：默认构造函数必须至少与基类型默认构造函数具有同样的关键性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DefaultConstructorsMustHaveConsistentTransparency|
|CheckId|CA2132|
|类别|Microsoft.Security|
|是否重大更改|重大|

> [!NOTE]
> 此警告仅适用于运行 CoreCLR 的代码（特定于 Silverlight Web 应用程序的 CLR 的版本）。

## <a name="cause"></a>原因
 派生类的默认构造函数的透明特性与基类的透明度不一样重要。

## <a name="rule-description"></a>规则说明
 Silverlight 应用程序代码不能使用具有 <xref:System.Security.SecurityCriticalAttribute> 的类型和成员。 安全关键类型和成员只能供 .NET Framework for Silverlight 类库中的受信任代码使用。 因为派生类中的某个公共或受保护构造必须有与其基类相同或更大的透明度，所以不能从标记为 SecurityCritical 的类派生应用程序中的类。

 对于 CoreCLR 平台代码，如果基类型具有公共或受保护的非透明默认构造函数，则派生类型必须遵循默认构造函数继承规则。 派生类型还必须具有默认的构造函数，并且该构造函数必须至少与基类型的关键默认构造函数相同。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此冲突，请删除该类型或不从安全非透明类型派生。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 请勿禁止显示此规则的警告。 应用程序代码违反此规则将导致 CoreCLR 拒绝使用 <xref:System.TypeLoadException> 加载该类型。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Security.CA2132.DefaultConstructorsMustHaveConsistentTransparency#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2132.defaultconstructorsmusthaveconsistenttransparency/cs/ca2132 - defaultconstructorsmusthaveconsistenttransparency.cs#1)]

### <a name="comments"></a>注释
