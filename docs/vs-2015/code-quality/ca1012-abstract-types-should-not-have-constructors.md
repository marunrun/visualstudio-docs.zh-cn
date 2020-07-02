---
title: CA1012：抽象类型不应具有构造函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AbstractTypesShouldNotHaveConstructors
- CA1012
helpviewer_keywords:
- CA1012
ms.assetid: 09f458ac-dd88-4cd7-a47f-4106c1e80ece
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 2c88144e788fb35a3c330aa28b4e9d8b91ff8003
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545452"
---
# <a name="ca1012-abstract-types-should-not-have-constructors"></a>CA1012:抽象类型不应具有构造函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|AbstractTypesShouldNotHaveConstructors|
|CheckId|CA1012|
|类别|Microsoft. Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 公共类型是抽象的，并且具有公共构造函数。

## <a name="rule-description"></a>规则描述
 抽象类型的构造函数只能由派生类型调用。 由于公共构造函数用于创建类型的实例，但无法为抽象类型创建实例，因此具有公共构造函数的抽象类在设计上是错误的。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请使构造函数成为受保护的，或者不将该类型声明为抽象类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 抽象类型具有公共构造函数。

## <a name="example"></a>示例
 下面的示例包含违反此规则的抽象类型。

 [!code-csharp[FxCop.Design.AbstractTypeBad#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AbstractTypeBad/cs/FxCop.Design.AbstractTypeBad.cs#1)]
 [!code-vb[FxCop.Design.AbstractTypeBad#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AbstractTypeBad/vb/FxCop.Design.AbstractTypeBad.vb#1)]

## <a name="example"></a>示例
 下面的示例通过将构造函数的可访问性从更改为来修复以前的冲突 `public` `protected` 。

 [!code-csharp[FxCop.Design.AbstractTypeGood#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AbstractTypeGood/cs/FxCop.Design.AbstractTypeGood.cs#1)]
 [!code-vb[FxCop.Design.AbstractTypeGood#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AbstractTypeGood/vb/FxCop.Design.AbstractTypeGood.vb#1)]
