---
title: CA1036:重写可比较类型的方法 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 49a4e64767497e4a1098bda9f5ee4e0eec8151f5
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65682821"
---
# <a name="ca1036-override-methods-on-comparable-types"></a>CA1036:重写可比较类型中的方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|OverrideMethodsOnComparableTypes|
|CheckId|CA1036|
|类别|Microsoft.Design|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 公共或受保护类型实现<xref:System.IComparable?displayProperty=fullName>接口，并不会覆盖<xref:System.Object.Equals%2A?displayProperty=fullName>或不会重载相等、 不等，小于或大于的特定于语言的运算符。 如果该类型继承接口的实现，该规则不报告冲突。

## <a name="rule-description"></a>规则说明
 定义自定义排序顺序的类型可实现<xref:System.IComparable>接口。 <xref:System.IComparable.CompareTo%2A>方法返回一个整数值，指示该类型的两个实例的正确的排序顺序。 此规则标识设置的排序顺序; 的类型这意味着，普通意义上的相等，不相等，小于且大于不适用于。 提供的实现时<xref:System.IComparable>，通常必须还重写<xref:System.Object.Equals%2A>，以便它将返回值与相一致<xref:System.IComparable.CompareTo%2A>。 如果重写<xref:System.Object.Equals%2A>进行编码和支持的运算符重载的语言，您还应提供与一致的运算符<xref:System.Object.Equals%2A>。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请重写<xref:System.Object.Equals%2A>。 如果您的编程语言支持运算符重载，提供以下运算符：

- op_Equality

- op_Inequality

- op_LessThan

- op_GreaterThan

  在 C# 中，用来表示这些运算符的令牌，如下所示为: = =、 ！ =、 \<，和 >。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告时冲突导致因缺少运算符和您的编程语言不支持运算符重载，可以使用 Visual Basic.NET 这种情况。 它也是安全地禁止显示此规则的警告，而不 op_Equality 如果你确定实现了运算符的应用程序上下文中不难理解它触发上相等运算符时。 但是，您应始终通过 op_Equality 和 = = 运算符，如果重写 Object.Equals。

## <a name="example"></a>示例
 下面的示例包含正确实现的类型<xref:System.IComparable>。 代码注释标识满足与相关的各种规则的方法<xref:System.Object.Equals%2A>和<xref:System.IComparable>接口。

 [!code-csharp[FxCop.Design.IComparable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IComparable/cs/FxCop.Design.IComparable.cs#1)]

## <a name="example"></a>示例
 下面的应用程序测试的行为<xref:System.IComparable>前面所示的实现。

 [!code-csharp[FxCop.Design.TestIComparable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestIComparable/cs/FxCop.Design.TestIComparable.cs#1)]

## <a name="see-also"></a>请参阅
 <xref:System.IComparable?displayProperty=fullName> <xref:System.Object.Equals%2A?displayProperty=fullName>
 [相等运算符](https://msdn.microsoft.com/library/bc496a91-fefb-4ce0-ab4c-61f09964119a)
