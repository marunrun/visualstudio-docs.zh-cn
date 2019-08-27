---
title: CA2229:实现序列化构造函数
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2229
- ImplementSerializationConstructors
helpviewer_keywords:
- CA2229
- ImplementSerializationConstructors
ms.assetid: 8e04d5fe-dfad-445a-972e-0648324fac45
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 11dfa98bb348f874a2774454cc465fb80cb71750
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920162"
---
# <a name="ca2229-implement-serialization-constructors"></a>CA2229:实现序列化构造函数

|||
|-|-|
|TypeName|ImplementSerializationConstructors|
|CheckId|CA2229|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
该类型实现<xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>接口, 不是委托或接口, 并且以下条件之一成立:

- 该类型没有采用<xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName>对象的构造函数和一个<xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>对象 (序列化构造函数的签名)。

- 类型是未密封的, 并且其序列化构造函数的访问修饰符是不受保护的 (系列)。

- 类型是密封的, 并且其序列化构造函数的访问修饰符不是私有的。

## <a name="rule-description"></a>规则说明
此规则适用于支持自定义序列化的类型。 如果类型实现<xref:System.Runtime.Serialization.ISerializable>接口, 则它支持自定义序列化。 序列化构造函数需要反序列化, 或者重新创建已使用<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName>方法进行序列化的对象。

## <a name="how-to-fix-violations"></a>如何解决冲突
要修复与该规则的冲突，请实现序列化构造函数。 对于密封类，请使构造函数成为私有；否则，请使构造函数成为受保护。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不要禁止违反规则。 该类型将不反序列化, 并且在许多情况下都不起作用。

## <a name="example"></a>示例
下面的示例演示一个满足规则的类型。

[!code-csharp[FxCop.Usage.ISerializableCtor#1](../code-quality/codesnippet/CSharp/ca2229-implement-serialization-constructors_1.cs)]

## <a name="related-rules"></a>相关规则
[CA2237：用 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

## <a name="see-also"></a>请参阅

- <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>
- <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName>
- <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>