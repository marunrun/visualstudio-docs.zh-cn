---
title: CA2300：请勿使用不安全的反序列化程序 BinaryFormatte
ms.date: 04/05/2019
ms.topic: reference
author: dotpaul
ms.author: paulming
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
f1_keywords:
- CA2300
- DoNotUseInsecureDeserializerBinaryFormatter
ms.openlocfilehash: 4ca4990308ceab21e2c6e256770ff37a3ca9a6fc
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71237943"
---
# <a name="ca2300-do-not-use-insecure-deserializer-binaryformatter"></a>CA2300：请勿使用不安全的反序列化程序 BinaryFormatte

|||
|-|-|
|TypeName|DoNotUseInsecureDeserializerBinaryFormatter|
|CheckId|CA2300|
|类别|Microsoft.Security|
|重大更改|不间断|

## <a name="cause"></a>原因

调用<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=nameWithType>或引用了反序列化方法。

## <a name="rule-description"></a>规则说明

[!INCLUDE[insecure-deserializers-description](includes/insecure-deserializers-description-md.md)]

此规则查找<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=nameWithType>反序列化方法调用或引用。 如果只希望在将<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Binder>属性设置为 "限制类型" 时进行反序列化，请禁用此规则并改为启用规则[CA2301](ca2301-do-not-call-binaryformatter-deserialize-without-first-setting-binaryformatter-binder.md)和[CA2302](ca2302-ensure-binaryformatter-binder-is-set-before-calling-binaryformatter-deserialize.md) 。

## <a name="how-to-fix-violations"></a>如何解决冲突

- 如果可能，请使用安全的序列化程序，而**不允许攻击者指定任意要反序列化的类型**。 一些更安全的序列化程序包括：
  - <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>
  - <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType>
  - <xref:System.Web.Script.Serialization.JavaScriptSerializer?displayProperty=nameWithType>-从不使用<xref:System.Web.Script.Serialization.SimpleTypeResolver?displayProperty=nameWithType>。 如果必须使用类型解析程序，请将反序列化类型限制为预期列表。
  - <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>
  - Newtonsoft.json Json.NET-使用 TypeNameHandling。 如果必须为 TypeNameHandling 使用其他值，请将反序列化类型限制为具有自定义 ISerializationBinder 的预期列表。
  - 协议缓冲区
- 使序列化的数据不会被篡改。 序列化后，对序列化的数据进行加密签名。 在反序列化之前，验证加密签名。 保护加密密钥不被泄露，并为密钥轮换设计。
- 限制反序列化的类型。 实现自定义<xref:System.Runtime.Serialization.SerializationBinder?displayProperty=nameWithType>。 使用<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>反序列化之前， <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Binder>请将属性设置为自定义<xref:System.Runtime.Serialization.SerializationBinder>的实例。 在重写<xref:System.Runtime.Serialization.SerializationBinder.BindToType%2A>的方法中，如果类型意外，将引发异常以停止反序列化。
  - 如果限制反序列化的类型，则可能需要禁用此规则并启用规则[CA2301](ca2301-do-not-call-binaryformatter-deserialize-without-first-setting-binaryformatter-binder.md)和[CA2302](ca2302-ensure-binaryformatter-binder-is-set-before-calling-binaryformatter-deserialize.md)。 规则[CA2301](ca2301-do-not-call-binaryformatter-deserialize-without-first-setting-binaryformatter-binder.md)和[CA2302](ca2302-ensure-binaryformatter-binder-is-set-before-calling-binaryformatter-deserialize.md)有助于<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Binder>确保始终在反序列化之前设置属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

[!INCLUDE[insecure-deserializers-common-safe-to-suppress](includes/insecure-deserializers-common-safe-to-suppress-md.md)]

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System.IO;
using System.Runtime.Serialization.Formatters.Binary;

public class ExampleClass
{
    public object MyDeserialize(byte[] bytes)
    {
        BinaryFormatter formatter = new BinaryFormatter();
        return formatter.Deserialize(new MemoryStream(bytes));
    }
}
```

```vb
Imports System.IO
Imports System.Runtime.Serialization.Formatters.Binary

Public Class ExampleClass
    Public Function MyDeserialize(bytes As Byte()) As Object
        Dim formatter As BinaryFormatter = New BinaryFormatter()
        Return formatter.Deserialize(New MemoryStream(bytes))
    End Function
End Class
```

## <a name="related-rules"></a>相关规则

[CA2301:请不要在不首先设置 BinaryFormatter 的情况下调用 BinaryFormatter](ca2301-do-not-call-binaryformatter-deserialize-without-first-setting-binaryformatter-binder.md)

[CA2302:请确保在调用 BinaryFormatter 之前设置 BinaryFormatter](ca2302-ensure-binaryformatter-binder-is-set-before-calling-binaryformatter-deserialize.md)