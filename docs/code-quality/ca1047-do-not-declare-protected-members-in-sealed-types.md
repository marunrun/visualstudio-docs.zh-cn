---
title: CA1047:不要在密封类型中声明受保护的成员
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DoNotDeclareProtectedMembersInSealedTypes
- CA1047
helpviewer_keywords:
- CA1047
- DoNotDeclareProtectedMembersInSealedTypes
ms.assetid: 829033b5-a9d8-4f26-a719-45494c9dd035
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 5ab7cf2c5a4f17966ed5b4da30657e05a4683738
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922650"
---
# <a name="ca1047-do-not-declare-protected-members-in-sealed-types"></a>CA1047:不要在密封类型中声明受保护的成员

|||
|-|-|
|TypeName|DoNotDeclareProtectedMembersInSealedTypes|
|CheckId|CA1047|
|类别|Microsoft.Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因
公共类型为 ( `sealed` `NotInheritable`在 Visual basic 中为), 并声明受保护的成员或受保护的嵌套类型。 此规则不报告<xref:System.Object.Finalize%2A>方法冲突, 这些方法必须遵循此模式。

## <a name="rule-description"></a>规则说明
类型声明受保护的成员，使继承类型可以访问或重写该成员。 按照定义, 不能从密封类型继承, 这意味着不能调用密封类型上的受保护方法。

C#编译器会发出此错误的警告。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请将成员的访问级别更改为 private, 或使该类型可继承。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。 使类型保持当前状态可能会导致维护问题, 而且不会带来任何好处。

## <a name="example"></a>示例
下面的示例演示违反此规则的类型。

[!code-vb[FxCop.Design.SealedNoProtected#1](../code-quality/codesnippet/VisualBasic/ca1047-do-not-declare-protected-members-in-sealed-types_1.vb)]
[!code-csharp[FxCop.Design.SealedNoProtected#1](../code-quality/codesnippet/CSharp/ca1047-do-not-declare-protected-members-in-sealed-types_1.cs)]