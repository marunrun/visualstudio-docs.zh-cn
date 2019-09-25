---
title: CA2235:标记所有不可序列化的字段
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2235
- MarkAllNonSerializableFields
helpviewer_keywords:
- CA2235
- MarkAllNonSerializableFields
ms.assetid: 599ad877-3a15-426c-bf17-5de15427365f
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 886cc66f820d201b8ab7f29fee00eebce07fc176
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71238100"
---
# <a name="ca2235-mark-all-non-serializable-fields"></a>CA2235:标记所有不可序列化的字段

|||
|-|-|
|TypeName|MarkAllNonSerializableFields|
|CheckId|CA2235|
|类别|Microsoft.Usage|
|重大更改|不间断|

## <a name="cause"></a>原因

在可以序列化的类型中声明了类型不可序列化的实例字段。

## <a name="rule-description"></a>规则说明

可序列化类型是用<xref:System.SerializableAttribute?displayProperty=fullName>特性标记的类型。 序列化类型时，如果该<xref:System.Runtime.Serialization.SerializationException?displayProperty=fullName>类型包含无法序列化*且*不实现<xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>接口的类型的实例字段，则会引发异常。

> [!TIP]
> 对于实现<xref:System.Runtime.Serialization.ISerializable>的类型的实例字段，不会激发 CA2235，因为它们提供了自己的序列化逻辑。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请<xref:System.NonSerializedAttribute?displayProperty=fullName>将属性应用于不可序列化的字段。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

仅当<xref:System.Runtime.Serialization.ISerializationSurrogate?displayProperty=fullName>声明的类型允许对字段的实例进行序列化和反序列化时，才禁止显示此规则发出的警告。

## <a name="example"></a>示例

下面的示例演示两种类型：一个违反规则的类型和一个满足规则的类型。

[!code-csharp[FxCop.Usage.MarkNonSerializable#1](../code-quality/codesnippet/CSharp/ca2235-mark-all-non-serializable-fields_1.cs)]
[!code-vb[FxCop.Usage.MarkNonSerializable#1](../code-quality/codesnippet/VisualBasic/ca2235-mark-all-non-serializable-fields_1.vb)]

## <a name="remarks"></a>备注

规则 CA2235 不分析实现<xref:System.Runtime.Serialization.ISerializable>接口的类型（除非它们也<xref:System.SerializableAttribute>用特性标记）。 这是因为[规则 CA2237](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)已建议用<xref:System.Runtime.Serialization.ISerializable> <xref:System.SerializableAttribute>特性来实现接口的标记类型。

## <a name="related-rules"></a>相关规则

- [CA2229：实现序列化构造函数](../code-quality/ca2229-implement-serialization-constructors.md)
- [CA2236对 ISerializable 类型调用基类方法](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)
- [CA2237：用 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)
- [CA2238正确实现序列化方法](../code-quality/ca2238-implement-serialization-methods-correctly.md)
- [CA2239为可选字段提供反序列化方法](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)
- [CA2240正确实现 ISerializable](../code-quality/ca2240-implement-iserializable-correctly.md)
- [CA2120保护序列化构造函数](../code-quality/ca2120-secure-serialization-constructors.md)