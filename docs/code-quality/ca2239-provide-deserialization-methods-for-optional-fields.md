---
title: CA2239:为可选字段提供反序列化方法
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2239
- ProvideDeserializationMethodsForOptionalFields
helpviewer_keywords:
- ProvideDeserializationMethodsForOptionalFields
- CA2239
ms.assetid: 6480ff5e-0caa-4707-814e-2f927cdafef5
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: c0cd59ec30ce45c94ac3422c4271959d74073bff
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920053"
---
# <a name="ca2239-provide-deserialization-methods-for-optional-fields"></a>CA2239:为可选字段提供反序列化方法

|||
|-|-|
|TypeName|ProvideDeserializationMethodsForOptionalFields|
|CheckId|CA2239|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
类型具有用<xref:System.Runtime.Serialization.OptionalFieldAttribute?displayProperty=fullName>特性标记的字段, 并且该类型不提供反序列化事件处理方法。

## <a name="rule-description"></a>规则说明
<xref:System.Runtime.Serialization.OptionalFieldAttribute>特性对序列化没有影响; 用特性标记的字段被序列化。 但是, 在反序列化时将忽略字段, 并保留与类型关联的默认值。 反序列化事件处理程序应该在反序列化过程中声明为设置字段。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请将反序列化事件处理方法添加到该类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果应该在反序列化过程中忽略该字段, 则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示一个具有可选字段和反序列化事件处理方法的类型。

[!code-csharp[FxCop.Usage.OptionalFields#1](../code-quality/codesnippet/CSharp/ca2239-provide-deserialization-methods-for-optional-fields_1.cs)]
[!code-vb[FxCop.Usage.OptionalFields#1](../code-quality/codesnippet/VisualBasic/ca2239-provide-deserialization-methods-for-optional-fields_1.vb)]

## <a name="related-rules"></a>相关规则
[CA2236对 ISerializable 类型调用基类方法](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

[CA2240正确实现 ISerializable](../code-quality/ca2240-implement-iserializable-correctly.md)

[CA2229：实现序列化构造函数](../code-quality/ca2229-implement-serialization-constructors.md)

[CA2238正确实现序列化方法](../code-quality/ca2238-implement-serialization-methods-correctly.md)

[CA2235：标记所有不可序列化的字段](../code-quality/ca2235-mark-all-non-serializable-fields.md)

[CA2237：用 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

[CA2120保护序列化构造函数](../code-quality/ca2120-secure-serialization-constructors.md)