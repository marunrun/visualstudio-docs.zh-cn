---
title: CA2132:默认构造函数必须至少与基类型默认构造函数为关键 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2132
ms.assetid: e758afa1-8bde-442a-8a0a-bd1ea7b0ce4d
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 8287fdf4c767e6fc2a41f014f724ab9a7fe61249
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385830"
---
# <a name="ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors"></a>CA2132:默认构造函数必须至少与基类型默认构造函数一样关键
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DefaultConstructorsMustHaveConsistentTransparency|
|CheckId|CA2132|
|类别|Microsoft.Security|
|是否重大更改|重大|

> [!NOTE]
> 此警告仅应用于运行 CoreCLR （Silverlight Web 应用程序特定的 CLR 的版本） 的代码。

## <a name="cause"></a>原因
 在派生类的默认构造函数的透明特性不是同样关键时基类的透明度。

## <a name="rule-description"></a>规则说明
 类型和成员具有<xref:System.Security.SecurityCriticalAttribute>Silverlight 应用程序代码不能使用。 安全关键类型和成员只能供 .NET Framework for Silverlight 类库中的受信任代码使用。 因为派生类中的某个公共或受保护构造必须有与其基类相同或更大的透明度，所以不能从标记为 SecurityCritical 的类派生应用程序中的类。

 对于 CoreCLR 平台代码，如果基类型具有公共或受保护的非透明默认构造函数然后派生的类型必须遵循的默认构造函数继承规则。 派生的类型还必须具有默认构造函数，该构造函数必须至少为基类型的关键的默认构造函数。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决冲突，请删除类型或不是从安全的非透明类型派生。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不要禁止显示此规则的警告。 违反此规则由应用程序代码将导致拒绝提供加载类型与 CoreCLR <xref:System.TypeLoadException>。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Security.CA2132.DefaultConstructorsMustHaveConsistentTransparency#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2132.defaultconstructorsmusthaveconsistenttransparency/cs/ca2132 - defaultconstructorsmusthaveconsistenttransparency.cs#1)]

### <a name="comments"></a>注释
