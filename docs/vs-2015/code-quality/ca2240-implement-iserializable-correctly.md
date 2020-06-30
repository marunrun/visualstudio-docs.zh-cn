---
title: CA2240：正确实现 ISerializable |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2240
- ImplementISerializableCorrectly
helpviewer_keywords:
- CA2240
- ImplementISerializableCorrectly
ms.assetid: cf05936d-0d6c-49ed-a1b4-220032e50b97
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 217f95b7d3658db107fc482040686eea9ee47604
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543658"
---
# <a name="ca2240-implement-iserializable-correctly"></a>CA2240:正确实现 ISerializable
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|ImplementISerializableCorrectly|
|CheckId|CA2240|
|Category|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 外部可见类型可分配给 <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> 接口，并满足以下条件之一：

- 该类型将继承，但不会重写 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName> 方法，并且该类型声明未标记为属性的实例字段 <xref:System.NonSerializedAttribute?displayProperty=fullName> 。

- 该类型不是密封的，并且该类型实现的 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> 方法不能在外部可见并且可重写。

## <a name="rule-description"></a>规则描述
 在继承接口的类型中声明的实例字段 <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> 不会自动包括在序列化过程中。 若要包含字段，类型必须实现 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> 方法和序列化构造函数。 如果不应序列化字段，请将属性应用于 <xref:System.NonSerializedAttribute> 字段以显式指示决策。

 在未密封的类型中，方法的实现 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> 应在外部可见。 因此，方法可由派生类型调用，并且是可重写的。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请使该 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> 方法可见并可重写，并确保所有实例字段都包括在序列化过程中，或者使用特性显式标记这些字段 <xref:System.NonSerializedAttribute> 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示两个与规则冲突的可序列化类型。

 [!code-cpp[FxCop.Usage.ImplementISerializableCorrectly#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly/cpp/FxCop.Usage.ImplementISerializableCorrectly.cpp#1)]
 [!code-csharp[FxCop.Usage.ImplementISerializableCorrectly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly/cs/FxCop.Usage.ImplementISerializableCorrectly.cs#1)]
 [!code-vb[FxCop.Usage.ImplementISerializableCorrectly#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly/vb/FxCop.Usage.ImplementISerializableCorrectly.vb#1)]

## <a name="example"></a>示例
 下面的示例通过提供 [GetObjectData] 的可替代实现来修复上述两个冲突（<!-- TODO: review code entity reference <xref:assetId:///ISerializable.GetObjectData?qualifyHint=False&amp;autoUpgrade=False>  -->）在 Book 类和的实现中提供 <!-- TODO: review code entity reference <xref:assetId:///ISerializable.GetObjectData?qualifyHint=False&amp;autoUpgrade=False>  --> 在库类中。

 [!code-cpp[FxCop.Usage.ImplementISerializableCorrectly2#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly2/cpp/FxCop.Usage.ImplementISerializableCorrectly2.cpp#1)]
 [!code-csharp[FxCop.Usage.ImplementISerializableCorrectly2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly2/cs/FxCop.Usage.ImplementISerializableCorrectly2.cs#1)]
 [!code-vb[FxCop.Usage.ImplementISerializableCorrectly2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly2/vb/FxCop.Usage.ImplementISerializableCorrectly2.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA2236:对 ISerializable 类型调用基类方法](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

 [CA2229:实现序列化构造函数](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238:正确实现序列化方法](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2235:标记所有不可序列化的字段](../code-quality/ca2235-mark-all-non-serializable-fields.md)

 [CA2237:用 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

 [CA2239:为可选字段提供反序列化方法](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)

 [CA2120:保护序列化构造函数](../code-quality/ca2120-secure-serialization-constructors.md)
