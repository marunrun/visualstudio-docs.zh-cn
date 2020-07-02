---
title: CA1903：仅使用目标框架中的 API |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseOnlyAPIFromTargetedFramework
- CA1903
helpviewer_keywords:
- UseOnlyApiFromTargetedFramework
- CA1903
ms.assetid: efdb5cc7-bbd8-4fa7-9fff-02b91e59350e
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 10649b4106a280089fd6b086167c7e92bff1300b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545244"
---
# <a name="ca1903-use-only-api-from-targeted-framework"></a>CA1903:仅使用目标框架中的 API
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有关 Visual Studio 的最新文档，请参阅[CA1903：仅使用目标框架中的 API](/visualstudio/code-quality/ca1903-use-only-api-from-targeted-framework)。

|项|值|
|-|-|
|TypeName|UseOnlyApiFromTargetedFramework|
|CheckId|CA1903|
|类别|Microsoft 可移植性|
|是否重大更改|正在进行-针对外部可见成员或类型的签名引发。<br /><br /> 不间断-在方法的主体中触发时。|

## <a name="cause"></a>原因
 成员或类型正在使用在项目的目标框架中未包含的 Service Pack 中引入的成员或类型。

## <a name="rule-description"></a>规则描述
 .NET Framework 2.0 Service Pack 1 和2、.NET Framework 3.0 Service Pack 1 和 2 .NET Framework 3.5 Service Pack 1 中包含新的成员和类型。 面向 .NET Framework 的主要版本的项目可能会无意中对这些新的 Api 进行依赖。 若要防止此依赖项，将在默认情况下对项目的目标框架不包含的任何新成员和类型使用情况触发此规则。

 **目标框架和 Service Pack 依赖项**

|项|值|
|-|-|
|当目标框架是|在中引入的成员的使用情况触发|
|.NET Framework 2.0|.NET Framework 2.0 SP1，.NET Framework 2.0 SP2|
|.NET Framework 3.0|.NET Framework 2.0 SP1，.NET Framework 2.0 SP2，.NET Framework 3.0 SP1，.NET Framework 3.0 SP2|
|.NET Framework 3.5|.NET Framework 3.5 SP1|
|.NET Framework 4|不可用|

 若要更改项目的目标框架，请参阅[面向特定 .NET Framework 版本](../ide/targeting-a-specific-dotnet-framework-version.md)。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要删除 Service Pack 的依赖项，请删除新成员或类型的所有使用实例。 如果这是有意的依赖项，请禁止显示此警告或关闭此规则。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果这不是对指定 Service Pack 的故意依赖项，请勿禁止显示此规则发出的警告。 在这种情况下，应用程序可能无法在未安装此 Service Pack 的系统上运行。 如果这是有意的依赖项，则禁止显示警告或关闭此规则。

## <a name="example"></a>示例
 下面的示例演示一个类，该类使用仅在 .NET 2.0 Service Pack 1 中可用的 DateTimeOffset 类型。 此示例要求在项目属性的 "目标框架" 下拉列表中选择 .NET Framework 2.0。

 [!code-csharp[FxCop.Portability.UseOnlyApiFromTargetedFramework#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Portability.UseOnlyApiFromTargetedFramework/CS/FxCop.Portability.UseOnlyApiFromTargetedFramework.cs#1)]

## <a name="example"></a>示例
 下面的示例通过将 DateTimeOffset 类型的用法替换为 DateTime 类型来修复前面描述的冲突。

 [!code-csharp[FxCop.Portability.UseOnlyApiFromTargetedFramework2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Portability.UseOnlyApiFromTargetedFramework2/CS/FxCop.Portability.UseOnlyApiFromTargetedFramework2.cs#1)]

## <a name="see-also"></a>另请参阅
 [面向特定 .NET Framework 版本的](../ide/targeting-a-specific-dotnet-framework-version.md)可[移植性警告](../code-quality/portability-warnings.md)
