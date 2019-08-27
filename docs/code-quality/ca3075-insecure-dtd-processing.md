---
title: CA3075:不安全的 DTD 处理
ms.date: 03/18/2019
ms.topic: reference
ms.assetid: 65798d66-7a30-4359-b064-61a8660c1eed
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6de817e3aaecbdd1c89cc2174e91126ea39d99d7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62541111"
---
# <a name="ca3075-insecure-dtd-processing"></a>CA3075:不安全的 DTD 处理

|||
|-|-|
|TypeName|InsecureDTDProcessing|
|CheckId|CA3075|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

如果使用不安全的 <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A> 实例或引用外部实体源，分析器可能会接受不受信任的输入并将敏感信息泄露给攻击者。

## <a name="rule-description"></a>规则说明

XML 分析器可以通过两种方式确定文档有效性， *文档类型定义 (DTD)* 是其中一种（根据  [万维网联合会 (W3C) 可扩展标记语言 (XML) 1.0](http://www.w3.org/TR/2008/REC-xml-20081126/)的定义）。 此规则查找某些属性和实例中接受不受信任的数据以提醒开发人员有关的潜在[信息泄露](/dotnet/framework/wcf/feature-details/information-disclosure)威胁或[拒绝服务 (DoS)](/dotnet/framework/wcf/feature-details/denial-of-service)攻击。 在以下情况下触发此规则：

- 在 <xref:System.Xml.XmlReader> 实例上启用了 DtdProcessing，它使用 <xref:System.Xml.XmlUrlResolver>解析外部 XML 实体。

- 设置了 XML 中的 <xref:System.Xml.XmlNode.InnerXml%2A> 属性。

- <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A> 属性设置为分析。

- 不受信任的使用处理输入<xref:System.Xml.XmlResolver>而不是<xref:System.Xml.XmlSecureResolver>。

- <xref:System.Xml.XmlReader.Create%2A?displayProperty=nameWithType>方法调用使用了不安全<xref:System.Xml.XmlReaderSettings>实例或根本没有实例。

- <xref:System.Xml.XmlReader> 使用不安全的默认设置或值创建。

在每个这种情况下，结果也是相同： 来自任一文件系统或网络共享从 XML 被处理的计算机的内容会公开给攻击者，或 DTD 处理可用作 DoS 向量。

## <a name="how-to-fix-violations"></a>如何解决冲突

- 捕获和处理所有 XmlTextReader 异常正确以避免路径信息泄露。

- 使用<xref:System.Xml.XmlSecureResolver>来限制 XmlTextReader 可以访问的资源。

- 通过将 <xref:System.Xml.XmlReader> 属性设置为 <xref:System.Xml.XmlResolver> null **，不允许**打开任何外部资源。

- 确保<xref:System.Data.DataViewManager.DataViewSettingCollectionString%2A?displayProperty=nameWithType>从受信任的源分配给属性。

**.NET 3.5 及更早版本**

- 禁用 DTD 处理，如果正在通过设置处理不可信的源<xref:System.Xml.XmlReaderSettings.ProhibitDtd%2A>属性设置为**true**。

- XmlTextReader 类具有完全信任继承要求。

**.NET 4 及更高版本**

- 避免启用 DtdProcessing，如果您正在处理不可信的源通过设置<xref:System.Xml.XmlReaderSettings.DtdProcessing%2A?displayProperty=nameWithType>属性设置为**禁止**或**忽略**。

- 确保在所有 InnerXml 用例中 load () 方法均采用 XmlReader 实例。

> [!NOTE]
> 此规则可能会针对某些有效 XmlSecureResolver 实例进行误报。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

除非确信已知道输入是来自受信任的源，否则请勿禁止显示此警告的规则。

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System.IO;
using System.Xml.Schema;

class TestClass
{
    public XmlSchema Test
    {
        get
        {
            var src = "";
            TextReader tr = new StreamReader(src);
            XmlSchema schema = XmlSchema.Read(tr, null); // warn
            return schema;
        }
    }
}
```

### <a name="solution"></a>解决方案

```csharp
using System.IO;
using System.Xml;
using System.Xml.Schema;

class TestClass
{
    public XmlSchema Test
    {
        get
        {
            var src = "";
            TextReader tr = new StreamReader(src);
            XmlTextReader reader = new XmlTextReader(tr) { DtdProcessing = DtdProcessing.Prohibit };
            XmlSchema schema = XmlSchema.Read(reader , null);
            return schema;
        }
    }
}
```

### <a name="violation"></a>冲突

```csharp
using System.Xml;

namespace TestNamespace
{
    public class TestClass
    {
        public XmlReaderSettings settings = new XmlReaderSettings();
        public void TestMethod(string path)
        {
            var reader = XmlReader.Create(path, settings);  // warn
        }
    }
}
```

### <a name="solution"></a>解决方案

```csharp
using System.Xml;

namespace TestNamespace
{
    public class TestClass
    {
        public XmlReaderSettings settings = new XmlReaderSettings()
        {
            DtdProcessing = DtdProcessing.Prohibit
        };

        public void TestMethod(string path)
        {
            var reader = XmlReader.Create(path, settings);
        }
    }
}
```

### <a name="violations"></a>冲突

```csharp
using System.Xml;

namespace TestNamespace
{
    public class DoNotUseSetInnerXml
    {
        public void TestMethod(string xml)
        {
            XmlDocument doc = new XmlDocument() { XmlResolver = null };
            doc.InnerXml = xml; // warn
        }
    }
}
```

```csharp
using System.Xml;

namespace TestNamespace
{
    public class DoNotUseLoadXml
    {
        public void TestMethod(string xml)
        {
            XmlDocument doc = new XmlDocument(){ XmlResolver = null };
            doc.LoadXml(xml); // warn
        }
    }
}
```

### <a name="solution"></a>解决方案

```csharp
using System.Xml;

public static void TestMethod(string xml)
{
    XmlDocument doc = new XmlDocument() { XmlResolver = null };
    System.IO.StringReader sreader = new System.IO.StringReader(xml);
    XmlReader reader = XmlReader.Create(sreader, new XmlReaderSettings() { XmlResolver = null });
    doc.Load(reader);
}
```

### <a name="violation"></a>冲突

```csharp
using System.IO;
using System.Xml;
using System.Xml.Serialization;

namespace TestNamespace
{
    public class UseXmlReaderForDeserialize
    {
        public void TestMethod(Stream stream)
        {
            XmlSerializer serializer = new XmlSerializer(typeof(UseXmlReaderForDeserialize));
            serializer.Deserialize(stream); // warn
        }
    }
}
```

### <a name="solution"></a>解决方案

```csharp
using System.IO;
using System.Xml;
using System.Xml.Serialization;

namespace TestNamespace
{
    public class UseXmlReaderForDeserialize
    {
        public void TestMethod(Stream stream)
        {
            XmlSerializer serializer = new XmlSerializer(typeof(UseXmlReaderForDeserialize));
            XmlReader reader = XmlReader.Create(stream, new XmlReaderSettings() { XmlResolver = null });
            serializer.Deserialize(reader );
        }
    }
}
```

### <a name="violation"></a>冲突

```csharp
using System.Xml;
using System.Xml.XPath;

namespace TestNamespace
{
    public class UseXmlReaderForXPathDocument
    {
        public void TestMethod(string path)
        {
            XPathDocument doc = new XPathDocument(path); // warn
        }
    }
}
```

### <a name="solution"></a>解决方案

```csharp
using System.Xml;
using System.Xml.XPath;

namespace TestNamespace
{
    public class UseXmlReaderForXPathDocument
    {
        public void TestMethod(string path)
        {
            XmlReader reader = XmlReader.Create(path, new XmlReaderSettings() { XmlResolver = null });
            XPathDocument doc = new XPathDocument(reader);
        }
    }
}
```

### <a name="violation"></a>冲突

```csharp
using System.Xml;

namespace TestNamespace
{
    class TestClass
    {
        public XmlDocument doc = new XmlDocument() { XmlResolver = new XmlUrlResolver() };
    }
}
```

### <a name="solution"></a>解决方案

```csharp
using System.Xml;

namespace TestNamespace
{
    class TestClass
    {
        public XmlDocument doc = new XmlDocument() { XmlResolver = null }; // or set to a XmlSecureResolver instance
    }
}
```

### <a name="violations"></a>冲突

```csharp
using System.Xml;

namespace TestNamespace
{
    class TestClass
    {
        private static void TestMethod()
        {
            var reader = XmlTextReader.Create(""doc.xml""); //warn
        }
    }
}
```

```csharp
using System.Xml;

namespace TestNamespace
{
    public class TestClass
    {
        public void TestMethod(string path)
        {
            try {
                XmlTextReader reader = new XmlTextReader(path); // warn
            }
            catch { throw ; }
            finally {}
        }
    }
}
```

### <a name="solution"></a>解决方案

```csharp
using System.Xml;

namespace TestNamespace
{
    public class TestClass
    {
        public void TestMethod(string path)
        {
            XmlReaderSettings settings = new XmlReaderSettings() { XmlResolver = null };
            XmlReader reader = XmlReader.Create(path, settings);
        }
    }
}
```
