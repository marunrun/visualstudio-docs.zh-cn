---
title: CA2237:用 SerializableAttribute 标记 ISerializable 类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2237
- MarkISerializableTypesWithSerializable
helpviewer_keywords:
- MarkISerializableTypesWithSerializable
- CA2237
ms.assetid: 9bd6bb24-a527-43dd-9952-043c0c694f46
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: f9d75a75449a07a5e9f651be0ba61598a29674ab
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201541"
---
# <a name="ca2237-mark-iserializable-types-with-serializableattribute"></a>CA2237:用 SerializableAttribute 标记 ISerializable 类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MarkISerializableTypesWithSerializable|
|CheckId|CA2237|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 外部可见的类型实现<xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>接口和类型未标有<xref:System.SerializableAttribute?displayProperty=fullName>属性。 规则将忽略其基类型不是可序列化的派生的类型。

## <a name="rule-description"></a>规则说明
 若要被公共语言运行时识别为可序列化，类型必须使用标记<xref:System.SerializableAttribute>属性，即使该类型使用通过实现一个自定义序列化例程<xref:System.Runtime.Serialization.ISerializable>接口。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请应用<xref:System.SerializableAttribute>属性的类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 因为它们必须序列化，以在应用程序域之间正常工作，不要禁止显示异常类的此规则的警告。

## <a name="example"></a>示例
 下面的示例显示了违反了此规则的类型。 取消注释<xref:System.SerializableAttribute>属性以满足该规则的行。

 [!code-csharp[FxCop.Usage.MarkSerializable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.MarkSerializable/cs/FxCop.Usage.MarkSerializable.cs#1)]
 [!code-vb[FxCop.Usage.MarkSerializable#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.MarkSerializable/vb/FxCop.Usage.MarkSerializable.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA2236:对 ISerializable 类型调用基类方法](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

 [CA2240:正确实现 ISerializable](../code-quality/ca2240-implement-iserializable-correctly.md)

 [CA2229：实现序列化构造函数](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238:正确实现序列化方法](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2235：标记所有不可序列化的字段](../code-quality/ca2235-mark-all-non-serializable-fields.md)

 [CA2239:提供反序列化方法为可选字段](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)

 [CA2120:安全的序列化构造函数](../code-quality/ca2120-secure-serialization-constructors.md)
