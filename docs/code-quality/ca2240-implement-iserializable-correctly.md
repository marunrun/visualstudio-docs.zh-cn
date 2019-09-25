---
title: CA2240:正确实现 ISerializable
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2240
- ImplementISerializableCorrectly
helpviewer_keywords:
- CA2240
- ImplementISerializableCorrectly
ms.assetid: cf05936d-0d6c-49ed-a1b4-220032e50b97
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 2640fddcde0d8777363a3c56e398e7ff307a20c7
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71237882"
---
# <a name="ca2240-implement-iserializable-correctly"></a>CA2240:正确实现 ISerializable

|||
|-|-|
|TypeName|ImplementISerializableCorrectly|
|CheckId|CA2240|
|类别|Microsoft.Usage|
|重大更改|不间断|

## <a name="cause"></a>原因

外部可见类型可分配给<xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>接口，并满足以下条件之一：

- 该类型将继承，但不会<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName>重写方法，并且该类型声明未标记<xref:System.NonSerializedAttribute?displayProperty=fullName>为属性的实例字段。

- 该类型不是密封的，并且该类型<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A>实现的方法不能在外部可见并且可重写。

## <a name="rule-description"></a>规则说明
在继承<xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>接口的类型中声明的实例字段不会自动包括在序列化过程中。 若要包含字段，类型必须实现<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A>方法和序列化构造函数。 如果不应序列化字段，请将<xref:System.NonSerializedAttribute>属性应用于字段以显式指示决策。

在未密封的类型中， <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A>方法的实现应在外部可见。 因此，方法可由派生类型调用，并且是可重写的。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A>使该方法可见并可重写，并确保所有实例字段都包括在序列化过程中<xref:System.NonSerializedAttribute> ，或者使用特性显式标记这些字段。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示两个与规则冲突的可序列化类型。

[!code-csharp[FxCop.Usage.ImplementISerializableCorrectly#1](../code-quality/codesnippet/CSharp/ca2240-implement-iserializable-correctly_1.cs)]
[!code-cpp[FxCop.Usage.ImplementISerializableCorrectly#1](../code-quality/codesnippet/CPP/ca2240-implement-iserializable-correctly_1.cpp)]
[!code-vb[FxCop.Usage.ImplementISerializableCorrectly#1](../code-quality/codesnippet/VisualBasic/ca2240-implement-iserializable-correctly_1.vb)]

## <a name="example"></a>示例
下面的示例通过在 Book 类上提供的<xref:System.Runtime.Serialization.ISerializable.GetObjectData>可替代实现并在库类上提供的`GetObjectData`实现来修复上述两个冲突。

[!code-cpp[FxCop.Usage.ImplementISerializableCorrectly2#1](../code-quality/codesnippet/CPP/ca2240-implement-iserializable-correctly_2.cpp)]
[!code-csharp[FxCop.Usage.ImplementISerializableCorrectly2#1](../code-quality/codesnippet/CSharp/ca2240-implement-iserializable-correctly_2.cs)]
[!code-vb[FxCop.Usage.ImplementISerializableCorrectly2#1](../code-quality/codesnippet/VisualBasic/ca2240-implement-iserializable-correctly_2.vb)]

## <a name="related-rules"></a>相关规则

- [CA2236对 ISerializable 类型调用基类方法](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)
- [CA2229：实现序列化构造函数](../code-quality/ca2229-implement-serialization-constructors.md)
- [CA2238正确实现序列化方法](../code-quality/ca2238-implement-serialization-methods-correctly.md)
- [CA2235：标记所有不可序列化的字段](../code-quality/ca2235-mark-all-non-serializable-fields.md)
- [CA2237：用 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)
- [CA2239为可选字段提供反序列化方法](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)
- [CA2120保护序列化构造函数](../code-quality/ca2120-secure-serialization-constructors.md)