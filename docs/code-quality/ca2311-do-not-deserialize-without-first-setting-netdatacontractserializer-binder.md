---
title: CA2311：在未先设置 NetDataContractSerializer.Binder 的情况下，请不要反序列化
ms.date: 05/01/2019
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
- CA2311
- DoNotDeserializeWithoutFirstSettingNetDataContractSerializerBinder
ms.openlocfilehash: 8445c6260592bbaf109dd3786111fe64441a4da0
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71237684"
---
# <a name="ca2311-do-not-deserialize-without-first-setting-netdatacontractserializerbinder"></a>CA2311：在未先设置 NetDataContractSerializer.Binder 的情况下，请不要反序列化

|||
|-|-|
|TypeName|DoNotDeserializeWithoutFirstSettingNetDataContractSerializerBinder|
|CheckId|CA2311|
|类别|Microsoft.Security|
|重大更改|不间断|

## <a name="cause"></a>原因

在未设置属性的<xref:System.Runtime.Serialization.NetDataContractSerializer.Binder>情况下调用或引用反序列化方法。<xref:System.Runtime.Serialization.NetDataContractSerializer?displayProperty=nameWithType>

## <a name="rule-description"></a>规则说明

[!INCLUDE[insecure-deserializers-description](includes/insecure-deserializers-description-md.md)]

此规则在<xref:System.Runtime.Serialization.NetDataContractSerializer?displayProperty=nameWithType>没有<xref:System.Runtime.Serialization.NetDataContractSerializer.Binder>设置时<xref:System.Runtime.Serialization.NetDataContractSerializer>查找反序列化方法调用或引用。 如果要禁止任何反序列<xref:System.Runtime.Serialization.NetDataContractSerializer>化，而不考虑<xref:System.Runtime.Serialization.NetDataContractSerializer.Binder>属性，请禁用此规则并[CA2312](ca2312-ensure-netdatacontractserializer-binder-is-set-before-deserializing.md)，并启用规则[CA2310](ca2310-do-not-use-insecure-deserializer-netdatacontractserializer.md)。

## <a name="how-to-fix-violations"></a>如何解决冲突

- 如果可能，请使用安全的序列化程序，而**不允许攻击者指定任意要反序列化的类型**。 一些更安全的序列化程序包括：
  - <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>
  - <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType>
  - <xref:System.Web.Script.Serialization.JavaScriptSerializer?displayProperty=nameWithType>-从不使用<xref:System.Web.Script.Serialization.SimpleTypeResolver?displayProperty=nameWithType>。 如果必须使用类型解析程序，请将反序列化类型限制为预期列表。
  - <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>
  - Newtonsoft.json Json.NET-使用 TypeNameHandling。 如果必须为 TypeNameHandling 使用其他值，请将反序列化类型限制为具有自定义 ISerializationBinder 的预期列表。
  - 协议缓冲区
- 使序列化的数据不会被篡改。 序列化后，对序列化的数据进行加密签名。 在反序列化之前，验证加密签名。 保护加密密钥不被泄露，并为密钥轮换设计。
- 限制反序列化的类型。 实现自定义<xref:System.Runtime.Serialization.SerializationBinder?displayProperty=nameWithType>。 使用<xref:System.Runtime.Serialization.NetDataContractSerializer>反序列化之前， <xref:System.Runtime.Serialization.NetDataContractSerializer.Binder>请将属性设置为自定义<xref:System.Runtime.Serialization.SerializationBinder>的实例。 在重写<xref:System.Runtime.Serialization.SerializationBinder.BindToType%2A>的方法中，如果类型意外，将引发异常以停止反序列化。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

[!INCLUDE[insecure-deserializers-common-safe-to-suppress](includes/insecure-deserializers-common-safe-to-suppress-md.md)]

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System;
using System.IO;
using System.Runtime.Serialization;

[DataContract]
public class BookRecord
{
    [DataMember]
    public string Title { get; set; }

    [DataMember]
    public string Author { get; set; }

    [DataMember]
    public int PageCount { get; set; }

    [DataMember]
    public AisleLocation Location { get; set; }
}

[DataContract]
public class AisleLocation
{
    [DataMember]
    public char Aisle { get; set; }

    [DataMember]
    public byte Shelf { get; set; }
}

public class ExampleClass
{
    public BookRecord DeserializeBookRecord(byte[] bytes)
    {
        NetDataContractSerializer serializer = new NetDataContractSerializer();
        using (MemoryStream ms = new MemoryStream(bytes))
        {
            return (BookRecord) serializer.Deserialize(ms);
        }
    }
}
```

```vb
Imports System
Imports System.IO
Imports System.Runtime.Serialization

<DataContract()>
Public Class BookRecord
    <DataMember()>
    Public Property Title As String

    <DataMember()>
    Public Property Author As String

    <DataMember()>
    Public Property Location As AisleLocation
End Class

<DataContract()>
Public Class AisleLocation
    <DataMember()>
    Public Property Aisle As Char

    <DataMember()>
    Public Property Shelf As Byte
End Class

Public Class ExampleClass
    Public Function DeserializeBookRecord(bytes As Byte()) As BookRecord
        Dim serializer As NetDataContractSerializer = New NetDataContractSerializer()
        Using ms As MemoryStream = New MemoryStream(bytes)
            Return CType(serializer.Deserialize(ms), BookRecord)
        End Using
    End Function
End Class
```

### <a name="solution"></a>解决方案

```csharp
using System;
using System.IO;
using System.Runtime.Serialization;

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

[DataContract]
public class BookRecord
{
    [DataMember]
    public string Title { get; set; }

    [DataMember]
    public string Author { get; set; }

    [DataMember]
    public int PageCount { get; set; }

    [DataMember]
    public AisleLocation Location { get; set; }
}

[DataContract]
public class AisleLocation
{
    [DataMember]
    public char Aisle { get; set; }

    [DataMember]
    public byte Shelf { get; set; }
}

public class ExampleClass
{
    public BookRecord DeserializeBookRecord(byte[] bytes)
    {
        NetDataContractSerializer serializer = new NetDataContractSerializer();
        serializer.Binder = new BookRecordSerializationBinder();
        using (MemoryStream ms = new MemoryStream(bytes))
        {
            return (BookRecord) serializer.Deserialize(ms);
        }
    }
}
```

```vb
Imports System
Imports System.IO
Imports System.Runtime.Serialization

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

<DataContract()>
Public Class BookRecord
    <DataMember()>
    Public Property Title As String

    <DataMember()>
    Public Property Author As String

    <DataMember()>
    Public Property Location As AisleLocation
End Class

<DataContract()>
Public Class AisleLocation
    <DataMember()>
    Public Property Aisle As Char

    <DataMember()>
    Public Property Shelf As Byte
End Class

Public Class ExampleClass
    Public Function DeserializeBookRecord(bytes As Byte()) As BookRecord
        Dim serializer As NetDataContractSerializer = New NetDataContractSerializer()
        serializer.Binder = New BookRecordSerializationBinder()
        Using ms As MemoryStream = New MemoryStream(bytes)
            Return CType(serializer.Deserialize(ms), BookRecord)
        End Using
    End Function
End Class
```

## <a name="related-rules"></a>相关规则

[CA2310:不要使用不安全的反序列化程序 NetDataContractSerializer](ca2310-do-not-use-insecure-deserializer-netdatacontractserializer.md)

[CA2312:确保在反序列化之前设置 NetDataContractSerializer](ca2312-ensure-netdatacontractserializer-binder-is-set-before-deserializing.md)