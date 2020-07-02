---
title: CA1021：避免参数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1021
- AvoidOutParameters
helpviewer_keywords:
- AvoidOutParameters
- CA1021
ms.assetid: 970f2304-842c-4fb7-9734-f3871da8d479
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f8f1b0c17fe9135bf534b9f30bf4e54c8c286ada
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546687"
---
# <a name="ca1021-avoid-out-parameters"></a>CA1021:避免使用 out 参数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|AvoidOutParameters|
|CheckId|CA1021|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共类型中的公共或受保护方法具有 `out` 参数。

## <a name="rule-description"></a>规则描述
 按引用传递类型（使用 `out` 或 `ref` ）需要使用指针的经验，了解值类型和引用类型的不同之处，以及处理具有多个返回值的方法。 此外，和参数之间的差异 `out` 并 `ref` 不被广泛理解。

 如果引用类型按引用传递，则该方法要使用参数来返回对象的不同实例。 按引用传递引用类型也称为使用双指针、指向指针的指针或双重间接寻址。 通过使用按值传递的默认调用约定 "，采用引用类型的参数已经收到指向对象的指针。 指针（而不是它指向的对象）通过值传递。 "按值传递" 表示方法不能更改指针以使其指向引用类型的新实例。 但是，它可以更改它所指向的对象的内容。 对于大多数应用程序，这就足够了，并生成了所需的行为。

 如果方法必须返回不同的实例，请使用方法的返回值来实现此目的。 有关对 <xref:System.String?displayProperty=fullName> 字符串执行操作并返回字符串的新实例的各种方法，请参阅类。 使用此模型时，调用方必须决定是否保留原始对象。

 尽管返回值非常常见并使用频繁，但正确应用 `out` 和 `ref` 参数需要中级设计和编码技能。 为一般受众设计的库架构师不应指望用户使用 `out` 或 `ref` 参数。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复由值类型引起的此规则的冲突，请让方法返回对象作为其返回值。 如果该方法必须返回多个值，请重新设计它以返回保存值的对象的单个实例。

 若要修复由引用类型引起的此规则的冲突，请确保所需的行为是返回引用的新实例。 如果是，则该方法应使用其返回值来执行此操作。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 可以安全地禁止显示此规则发出的警告。 但是，这种设计可能会导致可用性问题。

## <a name="example"></a>示例
 以下库显示类的两个实现，该类生成对用户反馈的响应。 第一个实现（ `BadRefAndOut` ）强制库用户管理三个返回值。 第二个实现（ `RedesignedRefAndOut` ）通过返回将 `ReplyData` 数据作为单个单元进行管理的容器类（）的实例，简化了用户体验。

 [!code-csharp[FxCop.Design.NoRefOrOut#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NoRefOrOut/cs/FxCop.Design.NoRefOrOut.cs#1)]

## <a name="example"></a>示例
 以下应用程序说明了用户的体验。 对重新设计的库（ `UseTheSimplifiedClass` 方法）的调用更简单，并且由方法返回的信息易于管理。 这两种方法的输出是相同的。

 [!code-csharp[FxCop.Design.TestNoRefOrOut#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestNoRefOrOut/cs/FxCop.Design.TestNoRefOrOut.cs#1)]

## <a name="example"></a>示例
 下面的示例库说明了如何 `ref` 使用引用类型的参数，并显示了实现此功能的更好方法。

 [!code-csharp[FxCop.Design.RefByRefNo#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.RefByRefNo/cs/FxCop.Design.RefByRefNo.cs#1)]

## <a name="example"></a>示例
 以下应用程序将调用库中的每个方法来演示行为。

 [!code-csharp[FxCop.Design.TestRefByRefNo#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestRefByRefNo/cs/FxCop.Design.TestRefByRefNo.cs#1)]

 本示例生成以下输出。

 **更改按值传递的指针：** 
**12345** 
**12345** 
**更改指针-通过引用传递：** 
**12345** 
**12345 abcde...z** 
**按返回值传递：** 
**12345 abcde...z**
## <a name="try-pattern-methods"></a>尝试模式方法

### <a name="description"></a>描述
 实现** \<Something> Try**模式的方法（如 <xref:System.Int32.TryParse%2A?displayProperty=fullName> ）不会引发此冲突。 下面的示例显示了实现方法的结构（值类型） <xref:System.Int32.TryParse%2A?displayProperty=fullName> 。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Design.TryPattern#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TryPattern/cs/FxCop.Design.TryPattern.cs#1)]

## <a name="related-rules"></a>相关规则
 [CA1045:不要通过引用来传递类型](../code-quality/ca1045-do-not-pass-types-by-reference.md)
