---
title: CA2235:标记所有不可序列化的字段 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2235
- MarkAllNonSerializableFields
helpviewer_keywords:
- CA2235
- MarkAllNonSerializableFields
ms.assetid: 599ad877-3a15-426c-bf17-5de15427365f
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 542ace3c1e73454884fb341f5f9e38cf09d86396
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201552"
---
# <a name="ca2235-mark-all-non-serializable-fields"></a>CA2235:标记所有不可序列化的字段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MarkAllNonSerializableFields|
|CheckId|CA2235|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 在可以序列化的类型中声明了类型不可序列化的实例字段。

## <a name="rule-description"></a>规则说明
 可序列化类型是指将标有<xref:System.SerializableAttribute?displayProperty=fullName>属性。 当序列化类型时，<xref:System.Runtime.Serialization.SerializationException?displayProperty=fullName>类型包含不可序列化的类型的实例字段而引发异常。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请应用<xref:System.NonSerializedAttribute?displayProperty=fullName>属性不是可序列化的字段。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果仅禁止显示此规则的警告<xref:System.Runtime.Serialization.ISerializationSurrogate?displayProperty=fullName>类型被声明为允许要进行序列化和反序列化的字段的实例。

## <a name="example"></a>示例
 下面的示例演示了违反规则的类型，并满足该规则的类型。

 [!code-csharp[FxCop.Usage.MarkNonSerializable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.MarkNonSerializable/cs/FxCop.Usage.MarkNonSerializable.cs#1)]
 [!code-vb[FxCop.Usage.MarkNonSerializable#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.MarkNonSerializable/vb/FxCop.Usage.MarkNonSerializable.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA2236:对 ISerializable 类型调用基类方法](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

 [CA2240:正确实现 ISerializable](../code-quality/ca2240-implement-iserializable-correctly.md)

 [CA2229：实现序列化构造函数](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238:正确实现序列化方法](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2237：用 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

 [CA2239:提供反序列化方法为可选字段](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)

 [CA2120:安全的序列化构造函数](../code-quality/ca2120-secure-serialization-constructors.md)
