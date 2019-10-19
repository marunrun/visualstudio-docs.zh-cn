---
title: CA2133：委托必须绑定到具有一致透明度的方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2133
ms.assetid: a09672e2-63cb-4abd-9e8f-dff515e101ce
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 487047b7dd3096e65a6e287d79d91d3029f3dc5a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72608986"
---
# <a name="ca2133-delegates-must-bind-to-methods-with-consistent-transparency"></a>CA2133：委托必须绑定到具有一致透明度的方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DelegatesMustBindWithConsistentTransparency|
|CheckId|CA2133|
|类别|Microsoft.Security|
|是否重大更改|重大|

> [!NOTE]
> 此警告仅适用于运行 CoreCLR 的代码（特定于 Silverlight Web 应用程序的 CLR 的版本）。

## <a name="cause"></a>原因
 此警告触发方法，该方法将标记有 <xref:System.Security.SecurityCriticalAttribute> 的委托绑定到透明或标记为 <xref:System.Security.SecuritySafeCriticalAttribute> 的方法。 还会对另一个具有以下特点的方法引发此警告：该方法将透明的或安全关键的委托绑定到一个关键方法。

## <a name="rule-description"></a>规则说明
 委托类型及其绑定到的方法必须具有一致的透明度。 透明和安全关键的委托只能绑定到其他透明或安全关键的方法。 同样，关键委托可能仅绑定到关键方法。 这些绑定规则确保唯一可以通过委托调用方法的代码也可以直接调用同一方法。 例如，绑定规则通过透明委托阻止透明代码直接调用关键代码。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此警告的冲突，请更改委托或它绑定的方法的透明度，使两者的透明度等效。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Security.CA2133.DelegatesMustBindWithConsistentTransparency#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2133.delegatesmustbindwithconsistenttransparency/cs/ca2133 - delegatesmustbindwithconsistenttransparency.cs#1)]
