---
title: CA1000:不要在泛型类型中声明静态成员
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1000
- DoNotDeclareStaticMembersOnGenericTypes
helpviewer_keywords:
- DoNotDeclareStaticMembersOnGenericTypes
- CA1000
ms.assetid: 5c0da594-f8d0-4f40-953d-56bf7fbd2087
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 4cc33c51af7d596fb9c784b76f8cc2f255ddf5a5
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236720"
---
# <a name="ca1000-do-not-declare-static-members-on-generic-types"></a>CA1000:不要在泛型类型中声明静态成员

|||
|-|-|
|TypeName|DoNotDeclareStaticMembersOnGenericTypes|
|CheckId|CA1000|
|类别|Microsoft.Design|
|重大更改|重大|

## <a name="cause"></a>原因

泛型类型包含`static` （`Shared`在 Visual Basic）成员中。

默认情况下，此规则仅查看外部可见类型，但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

当调用泛型类型的成员时，必须为该类型指定类型参数。`static` 当调用不支持推理的泛型实例成员时，必须指定该成员的类型参数。 在这两种情况下，在这两种情况中指定类型参数的语法不同，并且很容易混淆，如下所示：

```vb
' Shared method in a generic type.
GenericType(Of Integer).SharedMethod()

' Generic instance method that does not support inference.
someObject.GenericMethod(Of Integer)()
```

```csharp
// Static method in a generic type.
GenericType<int>.StaticMethod();

// Generic instance method that does not support inference.
someObject.GenericMethod<int>();
```

通常，应避免上述两个声明，以便在调用成员时不必指定类型参数。 这会导致在泛型中调用成员的语法与非泛型的语法不同。 有关详细信息，请[参阅 CA1004：泛型方法应提供类型参数](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请删除静态成员或将其更改为实例成员。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。 在易于理解和使用的语法中提供泛型，可减少学习和增加新库的采用率所需的时间。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)（而不是传统分析）运行此规则，则可以根据其可访问性，将基本代码的哪些部分配置为在上运行此规则。 例如，若要指定规则只应针对非公共 API 图面运行，请在项目中的 editorconfig 文件中添加以下键/值对：

```ini
dotnet_code_quality.ca1000.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则（设计）配置此选项。 有关详细信息，请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="related-rules"></a>相关规则

- [CA1005避免泛型类型的参数过多](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)
- [CA1010集合应实现泛型接口](../code-quality/ca1010-collections-should-implement-generic-interface.md)
- [CA1002不要公开泛型列表](../code-quality/ca1002-do-not-expose-generic-lists.md)
- [CA1006不要将泛型类型嵌套在成员签名中](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)
- [CA1004泛型方法应提供类型参数](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)
- [CA1003使用泛型事件处理程序实例](../code-quality/ca1003-use-generic-event-handler-instances.md)
- [CA1007在适当的位置使用泛型](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>请参阅

- [泛型](/dotnet/csharp/programming-guide/generics/index)