---
title: CA1036：重写可比较类型中的方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1036
- OverrideMethodsOnComparableTypes
helpviewer_keywords:
- OverrideMethodsOnComparableTypes
- CA1036
ms.assetid: 2329f844-4cb8-426d-bee2-cd065d1346d0
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 779e6258f9c5be256a7973a5d917045507fc82e6
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661829"
---
# <a name="ca1036-override-methods-on-comparable-types"></a>CA1036：重写可比较类型中的方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|OverrideMethodsOnComparableTypes|
|CheckId|CA1036|
|类别|Microsoft. Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 公共或受保护类型实现 <xref:System.IComparable?displayProperty=fullName> 接口，不会重写 <xref:System.Object.Equals%2A?displayProperty=fullName>，也不会重载语言特定的运算符是否相等、不相等、小于或大于。 如果类型仅继承接口的实现，则规则不会报告冲突。

## <a name="rule-description"></a>规则说明
 定义自定义排序顺序的类型实现 <xref:System.IComparable> 接口。 @No__t_0 方法返回一个整数值，该值指示类型的两个实例的正确排序顺序。 此规则标识设置排序顺序的类型;这意味着相等、不相等、小于和大于的普通含义不适用。 提供 <xref:System.IComparable> 的实现时，通常还必须重写 <xref:System.Object.Equals%2A>，以使其返回与 <xref:System.IComparable.CompareTo%2A> 一致的值。 如果重写 <xref:System.Object.Equals%2A> 并且是用支持运算符重载的语言编码的，则还应提供与 <xref:System.Object.Equals%2A> 一致的运算符。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请重写 <xref:System.Object.Equals%2A>。 如果编程语言支持运算符重载，请提供以下运算符：

- op_Equality

- op_Inequality

- op_LessThan

- op_GreaterThan

  在C#中，用于表示这些运算符的标记如下所示： = =、！ =、\< 和 >。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果冲突是由缺少运算符引起的，并且你的编程语言不支持运算符重载，则可以安全地禁止显示此规则发出的警告，这与 Visual Basic .NET 的情况相同。 如果你确定实现运算符在你的应用程序上下文中没有意义，则也可以安全地禁止显示此规则的警告。 但是，如果重写对象 Equals，应始终超过 op_Equality 和 = = 运算符。

## <a name="example"></a>示例
 下面的示例包含正确实现 <xref:System.IComparable> 的类型。 代码注释识别满足与 <xref:System.Object.Equals%2A> 和 <xref:System.IComparable> 接口相关的各种规则的方法。

 [!code-csharp[FxCop.Design.IComparable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IComparable/cs/FxCop.Design.IComparable.cs#1)]

## <a name="example"></a>示例
 下面的应用程序测试之前显示的 <xref:System.IComparable> 实现的行为。

 [!code-csharp[FxCop.Design.TestIComparable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestIComparable/cs/FxCop.Design.TestIComparable.cs#1)]

## <a name="see-also"></a>请参阅
 <xref:System.IComparable?displayProperty=fullName> <xref:System.Object.Equals%2A?displayProperty=fullName>
 [相等运算符](https://msdn.microsoft.com/library/bc496a91-fefb-4ce0-ab4c-61f09964119a)
