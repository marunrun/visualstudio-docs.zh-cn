---
title: CA2302：在调用 BinaryFormatter.Deserialize 之前，确保设置 BinaryFormatter.Binder
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
- CA2302
- EnsureBinaryFormatterBinderIsSetBeforeCallingBinaryFormatterDeserialize
ms.openlocfilehash: 1d7c87921a226b8918bfaa79fda6de85d710baa4
ms.sourcegitcommit: 673b9364fc9a96b027662dcb4cf5d61cab60ef11
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69891204"
---
# <a name="ca2302-ensure-binaryformatterbinder-is-set-before-calling-binaryformatterdeserialize"></a>CA2302：在调用 BinaryFormatter.Deserialize 之前，确保设置 BinaryFormatter.Binder

|||
|-|-|
|TypeName|EnsureBinaryFormatterBinderIsSetBeforeCallingBinaryFormatterDeserialize|
|CheckId|CA2302|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

调用<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=nameWithType>了反序列化方法, 或引用<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Binder>了该方法, 但该属性可以为 null。

## <a name="rule-description"></a>规则说明

[!INCLUDE[insecure-deserializers-description](includes/insecure-deserializers-description-md.md)]

此规则在<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=nameWithType> <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Binder>可能为 null 时查找反序列化方法调用或引用。 如果要禁止任何反序列<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>化, 而不考虑<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Binder>属性, 请禁用此规则并[CA2301](ca2301-do-not-call-binaryformatter-deserialize-without-first-setting-binaryformatter-binder.md), 并启用规则[CA2300](ca2300-do-not-use-insecure-deserializer-binaryformatter.md)。

## <a name="how-to-fix-violations"></a>如何解决冲突

- 如果可能, 请使用安全的序列化程序, 而**不允许攻击者指定任意要反序列化的类型**。 一些更安全的序列化程序包括:
  - <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>
  - <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType>
  - <xref:System.Web.Script.Serialization.JavaScriptSerializer?displayProperty=nameWithType>-从不使用<xref:System.Web.Script.Serialization.SimpleTypeResolver?displayProperty=nameWithType>。 如果必须使用类型解析程序, 请将反序列化类型限制为预期列表。
  - <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>
  - Newtonsoft.json Json.NET-使用 TypeNameHandling。 如果必须为 TypeNameHandling 使用其他值, 请将反序列化类型限制为具有自定义 ISerializationBinder 的预期列表。
  - 协议缓冲区
- 使序列化的数据不会被篡改。 序列化后, 对序列化的数据进行加密签名。 在反序列化之前, 验证加密签名。 保护加密密钥不被泄露, 并为密钥轮换设计。
- 限制反序列化的类型。 实现自定义<xref:System.Runtime.Serialization.SerializationBinder?displayProperty=nameWithType>。 使用<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>反序列化之前, <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Binder>请将属性设置为自定义<xref:System.Runtime.Serialization.SerializationBinder>的实例。 在重写<xref:System.Runtime.Serialization.SerializationBinder.BindToType%2A>的方法中, 如果类型意外, 将引发异常以停止反序列化。
  - 确保所有代码路径都设置了<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Binder>属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

[!INCLUDE[insecure-deserializers-common-safe-to-suppress](includes/insecure-deserializers-common-safe-to-suppress-md.md)]

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System;
using System.IO;
using System.Runtime.Serialization.Formatters.Binary;

[Serializable]
public class BookRecord
{
    public string Title { get; set; }
    public string Author { get; set; }
    public int PageCount { get; set; }
    public AisleLocation Location { get; set; }
}

[Serializable]
public class AisleLocation
{
    public char Aisle { get; set; }
    public byte Shelf { get; set; }
}

public class ExampleClass
{
    public BinaryFormatter Formatter { get; set; }

    public BookRecord DeserializeBookRecord(byte[] bytes)
    {
        using (MemoryStream ms = new MemoryStream(bytes))
        {
            return (BookRecord) this.Formatter.Deserialize(ms);
        }
    }
}
```

```vb
Imports System
Imports System.IO
Imports System.Runtime.Serialization.Formatters.Binary

<Serializable()>
Public Class BookRecord
    Public Property Title As String
    Public Property Author As String
    Public Property Location As AisleLocation
End Class

<Serializable()>
Public Class AisleLocation
    Public Property Aisle As Char
    Public Property Shelf As Byte
End Class

Public Class ExampleClass
    Public Property Formatter As BinaryFormatter

    Public Function DeserializeBookRecord(bytes As Byte()) As BookRecord
        Using ms As MemoryStream = New MemoryStream(bytes)
            Return CType(Me.Formatter.Deserialize(ms), BookRecord)
        End Using
    End Function
End Class
```

### <a name="solution"></a>解决方案

```csharp
using System;
using System.IO;
using System.Runtime.Serialization;
using System.Runtime.Serialization.Formatters.Binary;

public class BookRecordSerializationBinder : SerializationBinder
{
    public override Type BindToType(string assemblyName, string typeName)
    {
        // One way to discover expected types is through testing deserialization
        // of **valid** data and logging the types used.

        ////Console.WriteLine($"BindToType('{assemblyName}', '{typeName}')");

        if (typeName == "BookRecord" || typeName == "AisleLocation")
        {
            return null;
        }
        else
        {
            throw new ArgumentException("Unexpected type", nameof(typeName));
        }
    }
}

[Serializable]
public class BookRecord
{
    public string Title { get; set; }
    public string Author { get; set; }
    public int PageCount { get; set; }
    public AisleLocation Location { get; set; }
}

[Serializable]
public class AisleLocation
{
    public char Aisle { get; set; }
    public byte Shelf { get; set; }
}

public class ExampleClass
{
    public BookRecord DeserializeBookRecord(byte[] bytes)
    {
        BinaryFormatter formatter = new BinaryFormatter();
        formatter.Binder = new BookRecordSerializationBinder();
        using (MemoryStream ms = new MemoryStream(bytes))
        {
            return (BookRecord) formatter.Deserialize(ms);
        }
    }
}
```

```vb
Imports System
Imports System.IO
Imports System.Runtime.Serialization
Imports System.Runtime.Serialization.Formatters.Binary

Public Class BookRecordSerializationBinder
    Inherits SerializationBinder

    Public Overrides Function BindToType(assemblyName As String, typeName As String) As Type
        ' One way to discover expected types is through testing deserialization
        ' of **valid** data and logging the types used.

        'Console.WriteLine($"BindToType('{assemblyName}', '{typeName}')")

        If typeName = "BinaryFormatterVB.BookRecord" Or typeName = "BinaryFormatterVB.AisleLocation" Then
            Return Nothing
        Else
            Throw New ArgumentException("Unexpected type", NameOf(typeName))
        End If
    End Function
End Class

<Serializable()>
Public Class BookRecord
    Public Property Title As String
    Public Property Author As String
    Public Property Location As AisleLocation
End Class

<Serializable()>
Public Class AisleLocation
    Public Property Aisle As Char
    Public Property Shelf As Byte
End Class

Public Class ExampleClass
    Public Function DeserializeBookRecord(bytes As Byte()) As BookRecord
        Dim formatter As BinaryFormatter = New BinaryFormatter()
        formatter.Binder = New BookRecordSerializationBinder()
        Using ms As MemoryStream = New MemoryStream(bytes)
            Return CType(formatter.Deserialize(ms), BookRecord)
        End Using
    End Function
End Class
```

## <a name="related-rules"></a>相关规则

[CA2300:不要使用不安全的反序列化程序 BinaryFormatter](ca2300-do-not-use-insecure-deserializer-binaryformatter.md)

[CA2301:请不要在不首先设置 BinaryFormatter 的情况下调用 BinaryFormatter](ca2301-do-not-call-binaryformatter-deserialize-without-first-setting-binaryformatter-binder.md)
