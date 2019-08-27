---
title: CA1006:不要将泛型类型嵌套在成员签名中
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DoNotNestGenericTypesInMemberSignatures
- CA1006
helpviewer_keywords:
- CA1006
- DoNotNestGenericTypesInMemberSignatures
ms.assetid: dfc867bc-f4af-45d7-b071-db04a248f9fc
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 20bee606fd8cd98482a7304e068aaa7cbd5773a7
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923225"
---
# <a name="ca1006-do-not-nest-generic-types-in-member-signatures"></a>CA1006:不要将泛型类型嵌套在成员签名中

|||
|-|-|
|TypeName|DoNotNestGenericTypesInMemberSignatures|
|CheckId|CA1006|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
外部可见成员具有包含嵌套类型参数的签名。

## <a name="rule-description"></a>规则说明
嵌套类型参数是一个类型参数，也是一个泛型类型。 若要调用签名包含嵌套类型参数的成员，用户必须实例化一个泛型类型，并将此类型传递到另一个泛型类型的构造函数。 所需的过程和语法很复杂，应当避免。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请将设计更改为删除嵌套类型参数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。 在易于理解和使用的语法中提供泛型, 可减少学习和增加新库的采用率所需的时间。

## <a name="example"></a>示例
下面的示例演示一个方法, 该方法违反了规则, 以及调用违例方法所需的语法。

[!code-vb[FxCop.Design.NestedGenerics#1](../code-quality/codesnippet/VisualBasic/ca1006-do-not-nest-generic-types-in-member-signatures_1.vb)]
[!code-csharp[FxCop.Design.NestedGenerics#1](../code-quality/codesnippet/CSharp/ca1006-do-not-nest-generic-types-in-member-signatures_1.cs)]

## <a name="related-rules"></a>相关规则
[CA1005避免泛型类型的参数过多](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

[CA1010集合应实现泛型接口](../code-quality/ca1010-collections-should-implement-generic-interface.md)

[CA1000不要在泛型类型中声明静态成员](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

[CA1002不要公开泛型列表](../code-quality/ca1002-do-not-expose-generic-lists.md)

[CA1004泛型方法应提供类型参数](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

[CA1003使用泛型事件处理程序实例](../code-quality/ca1003-use-generic-event-handler-instances.md)

[CA1007在适当的位置使用泛型](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>请参阅
[泛型](/dotnet/csharp/programming-guide/generics/index)