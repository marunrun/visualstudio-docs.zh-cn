---
title: CA2123:重写链接请求应与基相同 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2123
- OverrideLinkDemandsShouldBeIdenticalToBase
helpviewer_keywords:
- OverrideLinkDemandsShouldBeIdenticalToBase
- CA2123
ms.assetid: 4538ecd5-fc6f-4480-ab00-90b2ce4730db
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 338d61db9c24972b7fef656498abd43f8ea0b976
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687225"
---
# <a name="ca2123-override-link-demands-should-be-identical-to-base"></a>CA2123:重写链接请求应与基相同
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|OverrideLinkDemandsShouldBeIdenticalToBase|
|CheckId|CA2123|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护方法的公共类型中重写的方法或实现一个接口，并且不具有相同[链接要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)作为接口或虚方法。

## <a name="rule-description"></a>规则说明
 该规则将一个方法与其基方法（该基方法为另一个类型中的接口或虚方法）相匹配，然后比较两者的链接请求。 如果在方法或基方法具有链接要求，并且另一个不会报告冲突。

 如果违反此规则，则恶意调用方只是调用不安全的方法，可以跳过链接要求。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请应用到重写方法或实现相同的链接要求。 如果无法做到这一点，此方法的完全要求标记或完全删除该属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示各种违反此规则。

 [!code-csharp[FxCop.Security.OverridesAndSecurity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.OverridesAndSecurity/cs/FxCop.Security.OverridesAndSecurity.cs#1)]

## <a name="see-also"></a>请参阅
 [安全编码准则](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)[链接需求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)
