---
title: CA2120:保护序列化构造函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2120
- SecureSerializationConstructors
helpviewer_keywords:
- SecureSerializationConstructors
- CA2120
ms.assetid: e9989da1-55a0-43f8-9aa9-da86afae3b41
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: ea70b7f9462e3195a78b915691a5069ebd6fe6aa
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154358"
---
# <a name="ca2120-secure-serialization-constructors"></a>CA2120:保护序列化构造函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|SecureSerializationConstructors|
|CheckId|CA2120|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 该类型实现<xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>接口，不是委托或接口，并允许部分受信任调用方的程序集中声明。 该类型具有一个构造函数采用<xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName>对象和一个<xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>对象 （序列化构造函数的签名）。 此构造函数不受安全检查，但一个或多个类型中的正则构造函数进行保护。

## <a name="rule-description"></a>规则说明
 此规则是适用于支持自定义序列化的类型。 类型支持自定义序列化，它实现了如果<xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>接口。 序列化构造函数是必需的用于反序列化，或重新创建对象已被序列化使用<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName>方法。 序列化构造函数分配并初始化对象，因为正则构造函数存在的安全检查也必须存在上序列化构造函数。 如果违反此规则，否则无法创建实例的调用方可以使用序列化构造函数来执行此操作。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，保护具有与保护其他构造函数相同的安全请求的序列化构造函数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不要禁止显示规则的冲突。

## <a name="example"></a>示例
 下面的示例显示了违反了此规则的类型。

 [!code-csharp[FxCop.Security.SerialCtors#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.SerialCtors/cs/FxCop.Security.SerialCtors.cs#1)]

## <a name="related-rules"></a>相关的规则
 [CA2229：实现序列化构造函数](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2237：用 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

## <a name="see-also"></a>请参阅
 <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName>
 <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>
