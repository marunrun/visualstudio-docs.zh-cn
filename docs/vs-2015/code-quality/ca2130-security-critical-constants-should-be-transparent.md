---
title: CA2130:安全关键常量应是透明 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2130
ms.assetid: 344c7f7b-9130-4675-ae7f-9fa260cc9789
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 26d3b5389bb080dee6e550c4bc0e6c035fd15db2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154336"
---
# <a name="ca2130-security-critical-constants-should-be-transparent"></a>CA2130:安全关键常量应是透明的
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ConstantsShouldBeTransparent|
|CheckId|CA2130|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 常量字段或枚举成员标记有<xref:System.Security.SecurityCriticalAttribute>。

## <a name="rule-description"></a>规则说明
 未对常数值实施透明强制，因为编译器内联常数值以便在运行时不需要查找。 常数字段应为安全透明的，以便代码评审阅者不会假定透明代码不能访问常数。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，请从字段或值中删除 SecurityCritical 属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 在下面的示例中，类型的枚举值`EnumWithCriticalValues.CriticalEnumValue`和常量`CriticalConstant`会发出此警告。 若要修复的问题，请删除 [`SecurityCritical`] 属性以使其安全透明。

 [!code-csharp[FxCop.Security.CA2130.ConstantsShouldBeTransparent#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2130.constantsshouldbetransparent/cs/ca2130 - constantsshouldbetransparent.cs#1)]
