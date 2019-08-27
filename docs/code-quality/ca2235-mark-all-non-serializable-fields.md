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
ms.openlocfilehash: 5ebfa5e9b90951acf59c8214941b93adae76d06e
ms.sourcegitcommit: 13ab9a5ab039b070b9cd9251d0b83dd216477203
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66177383"
---
# <a name="ca2235-mark-all-non-serializable-fields"></a>CA2235:标记所有不可序列化的字段

|||
|-|-|
|TypeName|MarkAllNonSerializableFields|
|CheckId|CA2235|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

在可以序列化的类型中声明了类型不可序列化的实例字段。

## <a name="rule-description"></a>规则说明

可序列化类型是指将标有<xref:System.SerializableAttribute?displayProperty=fullName>属性。 当序列化类型时，<xref:System.Runtime.Serialization.SerializationException?displayProperty=fullName>如果该类型包含不可序列化的类型的实例字段会引发异常*和*不会实现<xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>接口。

> [!TIP]
> CA2235 不会引发，例如实现的类型的字段<xref:System.Runtime.Serialization.ISerializable>因为它们提供其自己的序列化逻辑。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请应用<xref:System.NonSerializedAttribute?displayProperty=fullName>属性不是可序列化的字段。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果仅禁止显示此规则的警告<xref:System.Runtime.Serialization.ISerializationSurrogate?displayProperty=fullName>类型被声明为允许要进行序列化和反序列化的字段的实例。

## <a name="example"></a>示例

下面的示例演示两种类型： 一个违反了规则和一个满足该规则。

[!code-csharp[FxCop.Usage.MarkNonSerializable#1](../code-quality/codesnippet/CSharp/ca2235-mark-all-non-serializable-fields_1.cs)]
[!code-vb[FxCop.Usage.MarkNonSerializable#1](../code-quality/codesnippet/VisualBasic/ca2235-mark-all-non-serializable-fields_1.vb)]

## <a name="remarks"></a>备注

CA2235 不会分析实现的类型的规则<xref:System.Runtime.Serialization.ISerializable>接口 (除非它们还标记有<xref:System.SerializableAttribute>属性)。 这是因为[规则 CA2237](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)已建议标记类型实现<xref:System.Runtime.Serialization.ISerializable>接口与<xref:System.SerializableAttribute>属性。

## <a name="related-rules"></a>相关的规则

- [CA2229：实现序列化构造函数](../code-quality/ca2229-implement-serialization-constructors.md)
- [CA2236:对 ISerializable 类型调用基类方法](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)
- [CA2237：用 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)
- [CA2238:正确实现序列化方法](../code-quality/ca2238-implement-serialization-methods-correctly.md)
- [CA2239:提供反序列化方法为可选字段](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)
- [CA2240:正确实现 ISerializable](../code-quality/ca2240-implement-iserializable-correctly.md)
- [CA2120:安全的序列化构造函数](../code-quality/ca2120-secure-serialization-constructors.md)