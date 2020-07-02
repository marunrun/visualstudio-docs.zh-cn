---
title: CA2120：保护序列化构造函数 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 10cfa03adb74871fb42a6e1c2ce4ab4ba6bcae75
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544334"
---
# <a name="ca2120-secure-serialization-constructors"></a>CA2120:保护序列化构造函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|SecureSerializationConstructors|
|CheckId|CA2120|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 类型实现 <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> 接口，不是委托或接口，在允许部分受信任调用方的程序集中声明。 该类型具有一个构造函数，该构造函数采用一个 <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName> 对象和一个 <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName> 对象（序列化构造函数的签名）。 此构造函数不受安全检查的保护，但类型中的一个或多个常规构造函数受保护。

## <a name="rule-description"></a>规则描述
 此规则适用于支持自定义序列化的类型。 如果类型实现接口，则它支持自定义序列化 <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> 。 序列化构造函数是必需的，用于反序列化或重新创建已使用方法进行序列化的对象 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName> 。 因为序列化构造函数分配和初始化对象，所以在常规构造函数上存在的安全检查还必须存在于序列化构造函数中。 如果违反此规则，则无法以其他方式创建实例的调用方可以使用序列化构造函数来执行此操作。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请使用与保护其他构造函数相同的安全要求来保护序列化构造函数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不要禁止违反规则。

## <a name="example"></a>示例
 下面的示例演示违反规则的类型。

 [!code-csharp[FxCop.Security.SerialCtors#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.SerialCtors/cs/FxCop.Security.SerialCtors.cs#1)]

## <a name="related-rules"></a>相关规则
 [CA2229:实现序列化构造函数](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2237:用 SerializableAttribute 标记 ISerializable 类型](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

## <a name="see-also"></a>另请参阅
 <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName>
 <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>
