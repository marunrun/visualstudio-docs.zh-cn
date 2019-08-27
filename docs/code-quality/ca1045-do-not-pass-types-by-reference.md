---
title: CA1045:不要通过引用来传递类型
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1045
- DoNotPassTypesByReference
helpviewer_keywords:
- CA1045
- DoNotPassTypesByReference
ms.assetid: bcc3900a-e092-4bb8-896f-cb83f6289968
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6fd0da0f8b04055622b46087ecb9f12b375d9576
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922851"
---
# <a name="ca1045-do-not-pass-types-by-reference"></a>CA1045:不要通过引用来传递类型

|||
|-|-|
|TypeName|DoNotPassTypesByReference|
|CheckId|CA1045|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
公共类型中的公共或受保护方法具有一个`ref`参数, 该参数采用基元类型、引用类型或不属于内置类型的值类型。

## <a name="rule-description"></a>规则说明
按引用传递类型 (使用`out`或`ref`) 需要使用指针的经验, 了解值类型和引用类型的不同之处, 以及处理具有多个返回值的方法。 另外，`out` 和 `ref` 形参之间的区别并不广为人知。

如果引用类型按引用传递, 则该方法要使用参数来返回对象的不同实例。 (通过引用传递引用类型也称为使用双指针、指向指针的指针或双重间接寻址。)使用通过 "按值" 传递的默认调用约定, 采用引用类型的参数已经收到指向对象的指针。 指针 (而不是它指向的对象) 通过值传递。 通过值传递意味着该方法不能更改指针以使其指向引用类型的新实例, 但可以更改它所指向的对象的内容。 对于大多数应用程序, 这就足够了, 并生成了所需的行为。

如果方法必须返回不同的实例, 请使用方法的返回值来实现此目的。 有关对字符串执行操作并返回字符串的新实例的各种方法, 请参阅类。<xref:System.String?displayProperty=fullName> 通过使用此模型, 调用方可以决定是否保留原始对象。

尽管返回值非常常见并使用频繁, 但正确应用`out`和`ref`参数需要中级设计和编码技能。 为一般受众设计的库架构师不应指望用户`out`使用或`ref`参数。

> [!NOTE]
> 如果使用的参数是大型结构, 则在按值传递时, 复制这些结构所需的其他资源可能会导致性能影响。 在这些情况下, 可以考虑使用`ref`或`out`参数。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复由值类型引起的此规则的冲突, 请让方法返回对象作为其返回值。 如果该方法必须返回多个值, 请重新设计它以返回保存值的对象的单个实例。

若要修复由引用类型引起的此规则的冲突, 请确保所需的行为是返回引用的新实例。 如果是, 则该方法应使用其返回值来执行此操作。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
可以安全地禁止显示此规则发出的警告;但是, 这种设计可能会导致可用性问题。

## <a name="example"></a>示例
以下库显示类的两个实现, 该类生成对用户反馈的响应。 第一个实现 (`BadRefAndOut`) 强制库用户管理三个返回值。 第二个实现`RedesignedRefAndOut`() 通过返回将数据作为单个单元进行管理的容器类`ReplyData`() 的实例, 简化了用户体验。

[!code-csharp[FxCop.Design.NoRefOrOut#1](../code-quality/codesnippet/CSharp/ca1045-do-not-pass-types-by-reference_1.cs)]

## <a name="example"></a>示例
以下应用程序说明了用户的体验。 对重新设计的库 (`UseTheSimplifiedClass`方法) 的调用更简单, 并且由方法返回的信息易于管理。 这两种方法的输出是相同的。

[!code-csharp[FxCop.Design.TestNoRefOrOut#1](../code-quality/codesnippet/CSharp/ca1045-do-not-pass-types-by-reference_2.cs)]

## <a name="example"></a>示例
下面的示例库说明了`ref`如何使用引用类型的参数, 并显示了实现此功能的更好方法。

[!code-csharp[FxCop.Design.RefByRefNo#1](../code-quality/codesnippet/CSharp/ca1045-do-not-pass-types-by-reference_3.cs)]

## <a name="example"></a>示例
以下应用程序将调用库中的每个方法来演示行为。

[!code-csharp[FxCop.Design.TestRefByRefNo#1](../code-quality/codesnippet/CSharp/ca1045-do-not-pass-types-by-reference_4.cs)]

该示例产生下面的输出：

```txt
Changing pointer - passed by value:
12345
12345
Changing pointer - passed by reference:
12345
12345 ABCDE
Passing by return value:
12345 ABCDE
```

## <a name="related-rules"></a>相关规则
[CA1021避免输出参数](../code-quality/ca1021-avoid-out-parameters.md)