---
title: CA2146:类型必须至少与其基类型和接口一样关键 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2146
ms.assetid: 241fb784-1f6b-46e5-8ceb-c438e341d38e
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: d1a0120caf16fbed34fa87ab71fe50abc4467d51
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142659"
---
# <a name="ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces"></a>CA2146:类型必须至少与其基类型和接口一样关键
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|TypesMustBeAtLeastAsCriticalAsBaseTypes|
|CheckId|CA2146|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 透明类型派生自的类型将标有<xref:System.Security.SecuritySafeCriticalAttribute>或<xref:System.Security.SecurityCriticalAttribute>，或类型将标有<xref:System.Security.SecuritySafeCriticalAttribute>特性派生自的类型将标有<xref:System.Security.SecurityCriticalAttribute>属性。

## <a name="rule-description"></a>规则说明
 当派生类型具有的安全透明特性与其基类型或实现的接口不是同样关键时，将引发此规则。 只有关键类型可以从关键基类型派生或实现关键接口，并且只有关键或关键安全类型可以从安全关键基类型派生或实现关键安全接口。 违反此规则在级别 2 透明度导致<xref:System.TypeLoadException>派生的类型。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此冲突，标记是至少为基类型或接口一样关键的透明性属性的派生或实现类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 [!code-csharp[FxCop.Security.CA2146.TypesMustBeAtLeastAsCriticalAsBaseTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2146.typesmustbeatleastascriticalasbasetypes/cs/ca2146 - typesmustbeatleastascriticalasbasetypes.cs#1)]
