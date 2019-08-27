---
title: CA2240:正确实现 ISerializable |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 37f84bff4802c703bb61b36e9c1933a31cd6c5e3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142370"
---
# <a name="ca2240-implement-iserializable-correctly"></a>CA2240:正确实现 ISerializable
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ImplementISerializableCorrectly|
|CheckId|CA2240|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 外部可见的类型是分配给<xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>接口以及以下条件之一为 true:

- 该类型继承，但不重写<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName>方法和类型声明未标有实例字段<xref:System.NonSerializedAttribute?displayProperty=fullName>属性。

- 类型不密封的该类型实现<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A>不是外部可见且可重写的方法。

## <a name="rule-description"></a>规则说明
 实例继承的类型中声明的字段<xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>接口不自动包含在序列化过程。 若要包括的字段，该类型必须实现<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A>方法并序列化构造函数。 如果字段不应序列化，应用<xref:System.NonSerializedAttribute>属性要显式指示这一决定的字段。

 不密封的实现的类型中<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A>应外部可见方法。 因此，该方法可以由派生类型，调用，并且是可重写。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A>可见且可重写的方法，并确保所有实例字段要包含在序列化过程中或使用显式标记为<xref:System.NonSerializedAttribute>属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例显示了两个与该规则冲突的可序列化类型。

 [!code-cpp[FxCop.Usage.ImplementISerializableCorrectly#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly/cpp/FxCop.Usage.ImplementISerializableCorrectly.cpp#1)]
 [!code-csharp[FxCop.Usage.ImplementISerializableCorrectly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly/cs/FxCop.Usage.ImplementISerializableCorrectly.cs#1)]
 [!code-vb[FxCop.Usage.ImplementISerializableCorrectly#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly/vb/FxCop.Usage.ImplementISerializableCorrectly.vb#1)]

## <a name="example"></a>示例
 下面的示例通过提供可替代的 [ISerializable.GetObjectData] （实现修复前面两个冲突<!-- TODO: review code entity reference <xref:assetId:///ISerializable.GetObjectData?qualifyHint=False&amp;autoUpgrade=False>  -->) 在 Book 类，通过提供的实现 <!-- TODO: review code entity reference <xref:assetId:///ISerializable.GetObjectData?qualifyHint=False&amp;autoUpgrade=False>  --> 上的库类。

 [!code-cpp[FxCop.Usage.ImplementISerializableCorrectly2#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly2/cpp/FxCop.Usage.ImplementISerializableCorrectly2.cpp#1)]
 [!code-csharp[FxCop.Usage.ImplementISerializableCorrectly2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly2/cs/FxCop.Usage.ImplementISerializableCorrectly2.cs#1)]
 [!code-vb[FxCop.Usage.ImplementISerializableCorrectly2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly2/vb/FxCop.Usage.ImplementISerializableCorrectly2.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA2236:对 ISerializable 类型调用基类方法](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

 [CA2229：实现序列化构造函数](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238:正确实现序列化方法](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2235：标记所有不可序列化的字段](../code-quality/ca2235-mark-all-non-serializable-fields.md)

 [CA2237：用 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

 [CA2239:提供反序列化方法为可选字段](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)

 [CA2120:安全的序列化构造函数](../code-quality/ca2120-secure-serialization-constructors.md)
