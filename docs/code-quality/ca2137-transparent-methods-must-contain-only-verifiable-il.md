---
title: CA2137:透明方法只能包含可验证的 IL
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2137
ms.assetid: cbaeb0e1-56b6-43b4-812a-596b2859c329
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8ae8f507f17a1c64cb9fdfc5872ffa22e3c0f170
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232234"
---
# <a name="ca2137-transparent-methods-must-contain-only-verifiable-il"></a>CA2137:透明方法只能包含可验证的 IL

|||
|-|-|
|TypeName|TransparentMethodsMustBeVerifiable|
|CheckId|CA2137|
|类别|Microsoft.Security|
|重大更改|重大|

## <a name="cause"></a>原因
某个方法包含无法验证的代码或通过引用返回类型。

## <a name="rule-description"></a>规则说明
在尝试通过安全透明代码执行无法验证的 MSIL（Microsoft 中间语言）时将引发此规则。 但是，此规则不包含完整的 IL 验证程序，而是使用试探法来捕捉 MSIL 验证的大部分冲突。

若要确保您的代码仅包含可验证的 MSIL，请在程序集上运行[peverify.exe （Peverify.exe 工具）](/dotnet/framework/tools/peverify-exe-peverify-tool) 。 使用 **/transparent**选项运行 peverify.exe，该选项将输出限制为仅可验证的透明方法导致错误。 如果未使用/transparent 选项，则 Peverify.exe 还会验证允许包含无法验证的代码的关键方法。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请使用<xref:System.Security.SecurityCriticalAttribute>或<xref:System.Security.SecuritySafeCriticalAttribute>特性标记方法，或者删除无法验证的代码。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
此示例中的方法使用不可验证的代码，应使用<xref:System.Security.SecurityCriticalAttribute>或<xref:System.Security.SecuritySafeCriticalAttribute>特性进行标记。

[!code-csharp[FxCop.Security.CA2137.TransparentMethodsMustBeVerifiable#1](../code-quality/codesnippet/CSharp/ca2137-transparent-methods-must-contain-only-verifiable-il_1.cs)]