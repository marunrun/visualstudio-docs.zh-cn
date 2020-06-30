---
title: CA1005：避免泛型类型的参数过多 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidExcessiveParametersOnGenericTypes
- CA1005
helpviewer_keywords:
- AvoidExcessiveParametersOnGenericTypes
- CA1005
ms.assetid: 372b2f28-5c59-4815-9753-6c65b2bb3589
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 56c69badf76a05351b37a7c8a41a9cacf54f9974
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539719"
---
# <a name="ca1005-avoid-excessive-parameters-on-generic-types"></a>CA1005:避免泛型类型的参数过多
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|AvoidExcessiveParametersOnGenericTypes|
|CheckId|CA1005|
|Category|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见的泛型类型具有两个以上的类型参数。

## <a name="rule-description"></a>规则描述
 泛型类型包含的类型参数越多，越难以知道并记住每个类型参数各代表什么。 通常情况下，有一种类型参数（如中 `List<T>` ）和（在某些情况下有两个类型参数）非常明显，如中所示 `Dictionary<TKey, TValue>` 。 如果存在两个以上的类型参数，则很难为大多数用户（例如， `TooManyTypeParameters<T, K, V>` c # 中的或中的）变得过大 `TooManyTypeParameters(Of T, K, V)` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将设计更改为使用不超过两个类型参数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 请勿禁止显示此规则发出的警告，除非设计确实需要两个以上的类型参数。 在易于理解和使用的语法中提供泛型，可减少学习和增加新库的采用率所需的时间。

## <a name="related-rules"></a>相关规则
 [CA1010:集合应实现泛型接口](../code-quality/ca1010-collections-should-implement-generic-interface.md)

 [CA1000:不要在泛型类型中声明静态成员](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1002:不要公开泛型列表](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006:不要将泛型类型嵌套在成员签名中](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004:泛型方法应提供类型参数](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1003:使用泛型事件处理程序实例](../code-quality/ca1003-use-generic-event-handler-instances.md)

 [CA1007:在适用处使用泛型](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>另请参阅
 [泛型](https://msdn.microsoft.com/library/75ea8509-a4ea-4e7a-a2b3-cf72482e9282)
