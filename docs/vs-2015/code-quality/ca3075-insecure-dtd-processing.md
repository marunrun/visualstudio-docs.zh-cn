---
title: CA3075:不安全的 DTD 处理 |Microsoft Docs
ms.date: 11/15/2016
ms.technology: vs-ide-code-analysis
ms.topic: reference
ms.assetid: 65798d66-7a30-4359-b064-61a8660c1eed
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 694b72327d8e059fe12a227afdab79219081ef92
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65693412"
---
# <a name="ca3075-insecure-dtd-processing"></a>CA3075:不安全的 DTD 处理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|InsecureDTDProcessing|
|CheckId|CA3075|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 如果使用不安全的 <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A> 实例或引用外部实体源，分析器可能会接受不受信任的输入并将敏感信息泄露给攻击者。

## <a name="rule-description"></a>规则说明
 XML 分析器可以通过两种方式确定文档有效性， [文档类型定义 (DTD)](https://msdn.microsoft.com/library/aa468547.aspx) 是其中一种（根据  [万维网联合会 (W3C) 可扩展标记语言 (XML) 1.0](http://www.w3.org/TR/2008/REC-xml-20081126/)的定义）。 此规则查找接受不受信任数据的某些属性和实例以提醒开发人员有关的潜在 [Information Disclosure](https://msdn.microsoft.com/library/4064c89f-afa6-444a-aa7e-807ef072131c) 威胁，该威胁可能会导致 [拒绝服务 (DoS)](https://msdn.microsoft.com/library/dfb150f3-d598-4697-a5e6-6779e4f9b600) 攻击。 在以下情况下触发此规则：

- 在 <xref:System.Xml.XmlReader> 实例上启用了 DtdProcessing，它使用 <xref:System.Xml.XmlUrlResolver>解析外部 XML 实体。

- 设置了 XML 中的 <xref:System.Xml.XmlNode.InnerXml%2A> 属性。

- <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A> 属性设置为分析。

- 使用 <xref:System.Xml.XmlResolver> 而不是 <xref:System.Xml.XmlSecureResolver> 处理不受信任的输入。

- XmlReader。<xref:System.Xml.XmlReader.Create%2A> 方法使用了不安全调用<xref:System.Xml.XmlReaderSettings>实例或根本没有实例。

- <xref:System.Xml.XmlReader> 使用不安全的默认设置或值创建。

  在这些情况下，结果均相同：来自文件系统或来自处理 XML 的计算机的网络共享的文件都将面临攻击，其随后可能会被用作 DoS 向量。

## <a name="how-to-fix-violations"></a>如何解决冲突

- 捕获和处理所有 XmlTextReader 异常正确以避免路径信息泄露。

- 使用 <xref:System.Xml.XmlSecureResolver>来限制 XmlTextReader 可以访问的资源。

- 不允许 <xref:System.Xml.XmlReader>通过设置打开任何外部资源<xref:System.Xml.XmlResolver>属性设置为 **null**。

- 确保从可信的源分配 <xref:System.Data.DataViewManager.DataViewSettingCollectionString%2A> 的 <xref:System.Data.DataViewManager> 属性。

  .NET 3.5 及更早版本

- 禁用 DTD 处理，如果正在通过设置处理不可信的源 <xref:System.Xml.XmlReaderSettings.ProhibitDtd%2A>属性设置为 **true** 。

- XmlTextReader 类具有完全信任继承要求。 请参阅 [继承需求](https://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9)有关详细信息。

  .NET 4 及更高版本

- 如果正在处理不可信的源，请通过将 DtdProcessing 属性设置为 [禁止或忽略](https://msdn.microsoft.com/library/system.xml.dtdprocessing.aspx)避免启用 DtdProcessing。

- 确保在所有 InnerXml 用例中 load () 方法均采用 XmlReader 实例。

> [!NOTE]
> 此规则可能会针对某些有效 XmlSecureResolver 实例进行误报。 我们正在努力解决此问题，并预计于 2016 年中期之前解决此问题。

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
    XmlTextReader reader = new XmlTextReader(sreader) { DtdProcessing = DtdProcessing.Prohibit };
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
            XmlTextReader reader = new XmlTextReader(stream) { DtdProcessing = DtdProcessing.Prohibit } ;
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
            XmlTextReader reader = new XmlTextReader(path) { DtdProcessing = DtdProcessing.Prohibit };
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
    public class TestClass
    {
        public void TestMethod(string path)
        {
            XmlReaderSettings settings = new XmlReaderSettings(){ DtdProcessing = DtdProcessing.Parse };
            XmlReader reader = XmlReader.Create(path, settings); // warn
        }
    }
}
```

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
            XmlReaderSettings settings = new XmlReaderSettings(){ DtdProcessing = DtdProcessing.Prohibit };
            XmlReader reader = XmlReader.Create(path, settings);
        }
    }
}
```
