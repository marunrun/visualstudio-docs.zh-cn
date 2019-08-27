---
title: CA2222:不要递减继承的成员的可见性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotDecreaseInheritedMemberVisibility
- CA2222
helpviewer_keywords:
- DoNotDecreaseInheritedMemberVisibility
- CA2222
ms.assetid: 066c8675-381f-43cc-956c-d757cc494028
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: ee6228359e84687023a713ee866ebfbb760b206b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142461"
---
# <a name="ca2222-do-not-decrease-inherited-member-visibility"></a>CA2222:不要递减继承成员的可见性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotDecreaseInheritedMemberVisibility|
|CheckId|CA2222|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 非密封类型中的私有方法具有相同的基类型中声明的公共方法的签名。 私有方法不是最终的。

## <a name="rule-description"></a>规则说明
 不能更改所继承成员的访问修饰符。 将继承的成员更改为私有成员不能防止调用方访问该方法的基类实现。 如果成员设为私有且类型为未密封，继承类型可以调用继承层次结构中的最后一个公共方法的实现。 如果必须更改访问修饰符，则应最终标记的方法或应密封其类型以防止方法被重写。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请更改为非专用的访问权限。 或者，如果您的编程语言支持，您可以将此方法最终。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例显示了与此规则冲突的类型。

 [!code-csharp[FxCop.Usage.InheritedPublic#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.InheritedPublic/cs/FxCop.Usage.InheritedPublic.cs#1)]
 [!code-vb[FxCop.Usage.InheritedPublic#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.InheritedPublic/vb/FxCop.Usage.InheritedPublic.vb#1)]
