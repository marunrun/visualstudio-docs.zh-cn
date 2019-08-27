---
title: CA3076:不安全的 XSLT 脚本执行
ms.date: 11/04/2016
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5f98b022aef49a4d98ad4864793aa55732f8de6c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62541085"
---
# <a name="ca3076-insecure-xslt-script-execution"></a>CA3076:不安全的 XSLT 脚本执行

|||
|-|-|
|TypeName|InsecureXSLTScriptExecution|
|CheckId|CA3076|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

如果在 .NET 应用程序中不安全地执行可扩展样式表语言转换 (XSLT)，处理器可能会解析不受信任的 URI 引用，这种引用会把敏感信息泄露给攻击者，从而导致拒绝服务和跨站点攻击。 有关详细信息，请参阅[XSLT 安全 Considerations(.NET Guide)](/dotnet/standard/data/xml/xslt-security-considerations)。

## <a name="rule-description"></a>规则说明

**XSLT** 是万维网联合会 (W3C) 标准，用于转换 XML 数据。 XSLT 通常用于编写样式表转换为其他格式，如 HTML、 固定长度的文本、 以逗号分隔的文本或以不同的 XML 格式的 XML 数据。 尽管默认情况下禁止，你仍可以选择为项目启用该功能。

若要确保不会公开攻击面，此规则将触发每当 XslCompiledTransform。<xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> 接收的不安全组合实例<xref:System.Xml.Xsl.XsltSettings>和<xref:System.Xml.XmlResolver>，它允许处理恶意脚本。

## <a name="how-to-fix-violations"></a>如何解决冲突

- 不安全的 XsltSettings 参数替换为 XsltSettings。<xref:System.Xml.Xsl.XsltSettings.Default%2A> 或者与实例的已禁用文档函数和脚本执行。

- 将 <xref:System.Xml.XmlResolver> 参数替换为 null 或 <xref:System.Xml.XmlSecureResolver> 实例。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

除非确信已知道输入是来自受信任的源，否则请勿禁止显示此警告的规则。

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation-that-uses-xsltsettingstrustedxslt"></a>使用 XsltSettings.TrustedXslt 的冲突

```csharp
using System.Xml;
using System.Xml.Xsl;

namespace TestNamespace
{
    class TestClass
    {
         void TestMethod()
        {
             XslCompiledTransform xslCompiledTransform = new XslCompiledTransform();
             var settings = XsltSettings.TrustedXslt;
             var resolver = new XmlUrlResolver();
             xslCompiledTransform.Load("testStylesheet", settings, resolver); // warn
        }
    }
}
```

### <a name="solution-that-uses-xsltsettingsdefault"></a>使用 XsltSettings.Default 解决方案

```csharp
using System.Xml;
using System.Xml.Xsl;

namespace TestNamespace
{
    class TestClass
    {
        void TestMethod()
        {
            XslCompiledTransform xslCompiledTransform = new XslCompiledTransform();
            var settings = XsltSettings.Default;
            var resolver = new XmlUrlResolver();
            xslCompiledTransform.Load("testStylesheet", settings, resolver);
        }
    }
}
```

### <a name="violationmdashdocument-function-and-script-execution-not-disabled"></a>冲突&mdash;文档未禁用的函数和脚本执行

```csharp
using System.Xml;
using System.Xml.Xsl;

namespace TestNamespace
{
    class TestClass
    {
        private static void TestMethod(XsltSettings settings)
        {
            try
            {
                XslCompiledTransform xslCompiledTransform = new XslCompiledTransform();
                var resolver = new XmlUrlResolver();
                xslCompiledTransform.Load("testStylesheet", settings, resolver); // warn
            }
            catch { throw; }
            finally { }
        }
    }
}
```

### <a name="solutionmdashdisable-document-function-and-script-execution"></a>解决方案&mdash;禁用文档函数和脚本执行

```csharp
using System.Xml;
using System.Xml.Xsl;

namespace TestNamespace
{
    class TestClass
    {
        private static void TestMethod(XsltSettings settings)
        {
            try
            {
                XslCompiledTransform xslCompiledTransform = new XslCompiledTransform();
                settings.EnableDocumentFunction = false;
                settings.EnableScript = false;
                var resolver = new XmlUrlResolver();
                xslCompiledTransform.Load("testStylesheet", settings, resolver);
            }
            catch { throw; }
            finally { }
        }
    }
}
```

## <a name="see-also"></a>请参阅

- [XSLT 安全注意事项 （.NET 指南）](/dotnet/standard/data/xml/xslt-security-considerations)