---
title: CA2236：对 ISerializable 类型调用基类方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2236
- CallBaseClassMethodsOnISerializableTypes
helpviewer_keywords:
- CA2236
- CallBaseClassMethodsOnISerializableTypes
ms.assetid: 5a15b20d-769c-4640-b31a-36e07077daae
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1d06d4acff24b724388e36de66038f563b1f5dc6
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72666699"
---
# <a name="ca2236-call-base-class-methods-on-iserializable-types"></a>CA2236：对 ISerializable 类型调用基类方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|CallBaseClassMethodsOnISerializableTypes|
|CheckId|CA2236|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 类型派生自实现 <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> 接口的类型，并且满足以下条件之一：

- 该类型实现序列化构造函数，即，具有 <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName>、<xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName> 参数签名的构造函数，但不调用基类型的序列化构造函数。

- 该类型实现 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName> 方法，但不调用基类型的 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> 方法。

## <a name="rule-description"></a>规则说明
 在自定义序列化过程中，类型实现 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> 方法以序列化其字段，使用序列化构造函数对字段进行反序列化。 如果类型派生自实现 <xref:System.Runtime.Serialization.ISerializable> 接口的类型，则应调用基类型 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> 方法和序列化构造函数来序列化/反序列化基类型的字段。 否则，将不会正确序列化和反序列化该类型。 请注意，如果派生的类型不添加任何新字段，则类型不需要实现 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> 方法，也不需要调用序列化构造函数或调用等效的基类型。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请从相应的派生类型方法或构造函数调用基类型 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> 方法或序列化构造函数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示一个派生类型，它通过调用序列化构造函数和基类的 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> 方法来满足规则。

 [!code-csharp[FxCop.Usage.CallBaseISerializable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CallBaseISerializable/cs/FxCop.Usage.CallBaseISerializable.cs#1)]
 [!code-vb[FxCop.Usage.CallBaseISerializable#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CallBaseISerializable/vb/FxCop.Usage.CallBaseISerializable.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA2240：正确实现 ISerializable](../code-quality/ca2240-implement-iserializable-correctly.md)

 [CA2229：实现序列化构造函数](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238：正确实现序列化方法](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2235：标记所有不可序列化的字段](../code-quality/ca2235-mark-all-non-serializable-fields.md)

 [CA2237：以 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

 [CA2239：为可选字段提供反序列化方法](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)

 [CA2120：保护序列化构造函数](../code-quality/ca2120-secure-serialization-constructors.md)
