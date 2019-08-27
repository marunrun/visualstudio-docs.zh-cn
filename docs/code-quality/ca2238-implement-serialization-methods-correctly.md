---
title: CA2238:正确实现序列化方法
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- ImplementSerializationMethodsCorrectly
- CA2238
helpviewer_keywords:
- ImplementSerializationMethodsCorrectly
- CA2238
ms.assetid: 00882cf9-e10d-4d40-9126-3e6753e3c934
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: ec40eb3317f541bec92f06d8921fc2f545606d1a
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920089"
---
# <a name="ca2238-implement-serialization-methods-correctly"></a>CA2238:正确实现序列化方法

|||
|-|-|
|TypeName|ImplementSerializationMethodsCorrectly|
|CheckId|CA2238|
|类别|Microsoft.Usage|
|是否重大更改|如果方法在程序集外可见, 则为。<br /><br /> 否-如果该方法在程序集外部不可见, 则为。|

## <a name="cause"></a>原因
处理序列化事件的方法的签名、返回类型或可见性不正确。

## <a name="rule-description"></a>规则说明
通过应用以下序列化事件属性之一, 将方法指定为序列化事件处理程序:

- <xref:System.Runtime.Serialization.OnSerializingAttribute?displayProperty=fullName>

- <xref:System.Runtime.Serialization.OnSerializedAttribute?displayProperty=fullName>

- <xref:System.Runtime.Serialization.OnDeserializingAttribute?displayProperty=fullName>

- <xref:System.Runtime.Serialization.OnDeserializedAttribute?displayProperty=fullName>

  序列化事件处理程序采用类型<xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>为的单个参数, 返回`void`, `private`并具有可见性。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请更正序列化事件处理程序的签名、返回类型或可见性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示正确声明的序列化事件处理程序。

[!code-vb[FxCop.Usage.SerializationEventHandlers#1](../code-quality/codesnippet/VisualBasic/ca2238-implement-serialization-methods-correctly_1.vb)]
[!code-csharp[FxCop.Usage.SerializationEventHandlers#1](../code-quality/codesnippet/CSharp/ca2238-implement-serialization-methods-correctly_1.cs)]

## <a name="related-rules"></a>相关规则
[CA2236对 ISerializable 类型调用基类方法](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

[CA2240正确实现 ISerializable](../code-quality/ca2240-implement-iserializable-correctly.md)

[CA2229：实现序列化构造函数](../code-quality/ca2229-implement-serialization-constructors.md)

[CA2235：标记所有不可序列化的字段](../code-quality/ca2235-mark-all-non-serializable-fields.md)

[CA2237：用 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

[CA2239为可选字段提供反序列化方法](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)

 [CA2120保护序列化构造函数](../code-quality/ca2120-secure-serialization-constructors.md)