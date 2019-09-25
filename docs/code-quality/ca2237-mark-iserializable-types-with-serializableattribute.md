---
title: CA2237:用 SerializableAttribute 标记 ISerializable 类型
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2237
- MarkISerializableTypesWithSerializable
helpviewer_keywords:
- MarkISerializableTypesWithSerializable
- CA2237
ms.assetid: 9bd6bb24-a527-43dd-9952-043c0c694f46
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 53d049cad426201a8aaa48662061a4a424116b26
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71237932"
---
# <a name="ca2237-mark-iserializable-types-with-serializableattribute"></a>CA2237:用 SerializableAttribute 标记 ISerializable 类型

|||
|-|-|
|TypeName|MarkISerializableTypesWithSerializable|
|CheckId|CA2237|
|类别|Microsoft.Usage|
|重大更改|不间断|

## <a name="cause"></a>原因
外部可见类型实现<xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>接口，且类型没有<xref:System.SerializableAttribute?displayProperty=fullName>用特性标记。 规则将忽略基类型无法序列化的派生类型。

## <a name="rule-description"></a>规则说明
要由公共语言运行时识别为可序列化，即使类型通过实现<xref:System.SerializableAttribute> <xref:System.Runtime.Serialization.ISerializable>接口使用自定义序列化例程，也必须用特性标记类型。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请<xref:System.SerializableAttribute>将属性应用于该类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
请勿禁止显示此规则中的异常类的警告，因为它们必须是可序列化的，才能在应用程序域间正常工作。

## <a name="example"></a>示例
下面的示例演示违反规则的类型。 取消对<xref:System.SerializableAttribute>特性行的注释以满足规则。

[!code-vb[FxCop.Usage.MarkSerializable#1](../code-quality/codesnippet/VisualBasic/ca2237-mark-iserializable-types-with-serializableattribute_1.vb)]
[!code-csharp[FxCop.Usage.MarkSerializable#1](../code-quality/codesnippet/CSharp/ca2237-mark-iserializable-types-with-serializableattribute_1.cs)]

## <a name="related-rules"></a>相关规则
[CA2236对 ISerializable 类型调用基类方法](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

[CA2240正确实现 ISerializable](../code-quality/ca2240-implement-iserializable-correctly.md)

[CA2229：实现序列化构造函数](../code-quality/ca2229-implement-serialization-constructors.md)

[CA2238正确实现序列化方法](../code-quality/ca2238-implement-serialization-methods-correctly.md)

[CA2235：标记所有不可序列化的字段](../code-quality/ca2235-mark-all-non-serializable-fields.md)

[CA2239为可选字段提供反序列化方法](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)

[CA2120保护序列化构造函数](../code-quality/ca2120-secure-serialization-constructors.md)