---
title: CA2222:不要递减继承成员的可见性
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DoNotDecreaseInheritedMemberVisibility
- CA2222
helpviewer_keywords:
- DoNotDecreaseInheritedMemberVisibility
- CA2222
ms.assetid: 066c8675-381f-43cc-956c-d757cc494028
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: d63f4509872cc117ae03ff3a668d38a6efb07ef9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62541817"
---
# <a name="ca2222-do-not-decrease-inherited-member-visibility"></a>CA2222:不要递减继承成员的可见性

|||
|-|-|
|TypeName|DoNotDecreaseInheritedMemberVisibility|
|CheckId|CA2222|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

非密封类型中的私有方法具有相同的基类型中声明的公共方法的签名。 私有方法不是最终的。

## <a name="rule-description"></a>规则说明

不会更改继承的成员访问修饰符。 将继承的成员更改为私有成员不能防止调用方访问该方法的基类实现。 如果成员设为私有且类型为未密封，继承类型可以调用继承层次结构中的最后一个公共方法的实现。 如果必须更改访问修饰符，则应最终标记的方法或应密封其类型以防止方法被重写。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请更改为非专用的访问权限。 或者，如果您的编程语言支持，您可以将此方法最终。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。

## <a name="example"></a>示例

下面的示例显示了与此规则冲突的类型。

[!code-vb[FxCop.Usage.InheritedPublic#1](../code-quality/codesnippet/VisualBasic/ca2222-do-not-decrease-inherited-member-visibility_1.vb)]
[!code-csharp[FxCop.Usage.InheritedPublic#1](../code-quality/codesnippet/CSharp/ca2222-do-not-decrease-inherited-member-visibility_1.cs)]