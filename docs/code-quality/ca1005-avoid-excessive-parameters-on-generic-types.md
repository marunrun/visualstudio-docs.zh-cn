---
title: CA1005:避免泛型类型的参数过多
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AvoidExcessiveParametersOnGenericTypes
- CA1005
helpviewer_keywords:
- AvoidExcessiveParametersOnGenericTypes
- CA1005
ms.assetid: 372b2f28-5c59-4815-9753-6c65b2bb3589
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 34f9b8a79e38bdb9b6b097588697e2cd6c3545f7
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236597"
---
# <a name="ca1005-avoid-excessive-parameters-on-generic-types"></a>CA1005:避免泛型类型的参数过多

|||
|-|-|
|TypeName|AvoidExcessiveParametersOnGenericTypes|
|CheckId|CA1005|
|类别|Microsoft.Design|
|重大更改|重大|

## <a name="cause"></a>原因
外部可见的泛型类型具有两个以上的类型参数。

## <a name="rule-description"></a>规则说明
泛型类型包含的类型参数越多，越难以知道并记住每个类型参数各代表什么。 通常情况下，有一种类型参数（如`List<T>`中）和（在某些情况下有两个类型`Dictionary<TKey, TValue>`参数）非常明显，如中所示。 如果存在两个以上的类型参数，则很难为大多数用户（例如`TooManyTypeParameters<T, K, V>` ，在C#或`TooManyTypeParameters(Of T, K, V)`中[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]为）。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请将设计更改为使用不超过两个类型参数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
请勿禁止显示此规则发出的警告，除非设计确实需要两个以上的类型参数。 在易于理解和使用的语法中提供泛型，可减少学习和增加新库的采用率所需的时间。

## <a name="related-rules"></a>相关规则
[CA1010集合应实现泛型接口](../code-quality/ca1010-collections-should-implement-generic-interface.md)

[CA1000不要在泛型类型中声明静态成员](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

[CA1002不要公开泛型列表](../code-quality/ca1002-do-not-expose-generic-lists.md)

[CA1006不要将泛型类型嵌套在成员签名中](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

[CA1004泛型方法应提供类型参数](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

[CA1003使用泛型事件处理程序实例](../code-quality/ca1003-use-generic-event-handler-instances.md)

[CA1007在适当的位置使用泛型](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>请参阅
[泛型](/dotnet/csharp/programming-guide/generics/index)