---
title: CA1021:避免使用 out 参数 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: b52d5a97fc3c2e3a6bf5b4bb938bad9da50d3a7d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68144826"
---
# <a name="ca1021-avoid-out-parameters"></a>CA1021:避免使用 out 参数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidOutParameters|
|CheckId|CA1021|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护方法的公共类型中具有`out`参数。

## <a name="rule-description"></a>规则说明
 通过引用传递类型 (使用`out`或`ref`) 需要体验提供了指导，了解值类型和引用类型的不同之处，以及能处理具有多个返回值的方法。 另外，`out` 和 `ref` 形参之间的区别并不广为人知。

 当"按引用"传递引用类型时，方法将希望使用参数可返回对象的不同实例。 按引用传递引用类型也称为使用双指针、 指向指针的指针或双间接寻址。 通过使用的默认调用约定，通过"按值"，已采用引用类型参数接收指向对象的指针。 按值传递的指针，它指向的而非对象。 通过此方法不能更改要将其指向引用类型的新实例的指针的值表示传递。 但是，它可以更改它所指向的对象的内容。 对于大多数应用程序这就足够了，并生成所需的行为。

 如果一种方法必须返回不同的实例，使用该方法的返回值来实现此目的。 请参阅<xref:System.String?displayProperty=fullName>类的各种方法对字符串执行操作并返回一个字符串的新实例。 使用此模型时，调用方必须决定是否保留原始对象。

 尽管比较常见并大量使用正确的应用程序的返回值`out`和`ref`参数需要中间设计和编码技能。 库设计为普通用户不应指望用户掌握了架构师`out`或`ref`参数。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与由值类型导致此规则的冲突，使该方法返回的对象作为其返回值。 如果该方法必须返回多个值，重新设计它返回一个对象，保存值的单个实例。

 若要修复的由引用类型导致此规则冲突，请确保所需的行为是返回引用的新实例。 如果是，该方法应使用它的返回值来执行此操作。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告。 但是，这种设计可能会导致可用性问题。

## <a name="example"></a>示例
 以下库将显示生成的用户的反馈响应的类的两种实现。 第一种实现 (`BadRefAndOut`) 强制库用户可以管理三个返回值。 第二个实现 (`RedesignedRefAndOut`) 通过返回容器类的实例来简化用户体验 (`ReplyData`) 管理作为一个单元的数据。

 [!code-csharp[FxCop.Design.NoRefOrOut#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NoRefOrOut/cs/FxCop.Design.NoRefOrOut.cs#1)]

## <a name="example"></a>示例
 下面的应用程序说明了用户体验。 重新设计的库的调用 (`UseTheSimplifiedClass`方法) 更简单且易于管理的方法返回的信息。 两种方法的输出是相同的。

 [!code-csharp[FxCop.Design.TestNoRefOrOut#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestNoRefOrOut/cs/FxCop.Design.TestNoRefOrOut.cs#1)]

## <a name="example"></a>示例
 下面的示例库说明了如何`ref`对于引用类型参数使用，并演示更好的方法来实现此功能。

 [!code-csharp[FxCop.Design.RefByRefNo#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.RefByRefNo/cs/FxCop.Design.RefByRefNo.cs#1)]

## <a name="example"></a>示例
 下面的应用程序调用来演示该行为的库中的每个方法。

 [!code-csharp[FxCop.Design.TestRefByRefNo#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestRefByRefNo/cs/FxCop.Design.TestRefByRefNo.cs#1)]

 本示例生成以下输出。

 **更改指针的按值传递：** 
**12345**
**12345**
**更改指针的按引用传递：** 
**12345**
**12345 ABCDE**
**传递返回值：** 
**12345 ABCDE**
## <a name="try-pattern-methods"></a>请尝试模式方法

### <a name="description"></a>描述
 实现的方法**尝试\<内容 >** 模式，如<xref:System.Int32.TryParse%2A?displayProperty=fullName>，不会引发此冲突。 下面的示例演示实现的结构 （值类型）<xref:System.Int32.TryParse%2A?displayProperty=fullName>方法。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Design.TryPattern#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TryPattern/cs/FxCop.Design.TryPattern.cs#1)]

## <a name="related-rules"></a>相关的规则
 [CA1045:不要通过引用来传递类型](../code-quality/ca1045-do-not-pass-types-by-reference.md)
