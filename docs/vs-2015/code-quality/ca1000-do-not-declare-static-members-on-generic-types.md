---
title: CA1000：不要在泛型类型上声明静态成员 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1000
- DoNotDeclareStaticMembersOnGenericTypes
helpviewer_keywords:
- DoNotDeclareStaticMembersOnGenericTypes
- CA1000
ms.assetid: 5c0da594-f8d0-4f40-953d-56bf7fbd2087
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 66bca5b8b039de59509cecf4ecfae6bd6b4f0162
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548325"
---
# <a name="ca1000-do-not-declare-static-members-on-generic-types"></a>CA1000:不要在泛型类型中声明静态成员
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|DoNotDeclareStaticMembersOnGenericTypes|
|CheckId|CA1000|
|Category|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见的泛型类型包含 `static` （ `Shared` 在 Visual Basic）成员中。

## <a name="rule-description"></a>规则描述
 当 `static` 调用泛型类型的成员时，必须为该类型指定类型参数。 当调用不支持推理的泛型实例成员时，必须指定该成员的类型参数。 在这两种情况下，在这两种情况中指定类型参数的语法不同，并且很容易混淆，如下所示：

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

 通常，应避免上述两个声明，以便在调用成员时不必指定类型参数。 这会导致在泛型中调用成员的语法与非泛型的语法不同。 有关详细信息，请参阅[CA1004：泛型方法应提供类型参数](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请删除静态成员或将其更改为实例成员。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 在易于理解和使用的语法中提供泛型，可减少学习和增加新库的采用率所需的时间。

## <a name="related-rules"></a>相关规则
 [CA1005:避免泛型类型的参数过多](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1010:集合应实现泛型接口](../code-quality/ca1010-collections-should-implement-generic-interface.md)

 [CA1002:不要公开泛型列表](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006:不要将泛型类型嵌套在成员签名中](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004:泛型方法应提供类型参数](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1003:使用泛型事件处理程序实例](../code-quality/ca1003-use-generic-event-handler-instances.md)

 [CA1007:在适用处使用泛型](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>另请参阅
 [泛型](https://msdn.microsoft.com/library/75ea8509-a4ea-4e7a-a2b3-cf72482e9282)
