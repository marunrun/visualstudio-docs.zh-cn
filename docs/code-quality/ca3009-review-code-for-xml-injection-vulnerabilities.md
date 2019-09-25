---
title: CA3009：查看 XML 注入漏洞的代码
ms.date: 04/03/2019
ms.topic: reference
author: dotpaul
ms.author: paulming
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 37ba7e8664c6fa24e302dbebd38643a0c451114c
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71237247"
---
# <a name="ca3009-review-code-for-xml-injection-vulnerabilities"></a>CA3009：查看 XML 注入漏洞的代码

|||
|-|-|
|TypeName|ReviewCodeForXmlInjectionVulnerabilities|
|CheckId|CA3009|
|类别|Microsoft.Security|
|重大更改|不间断|

## <a name="cause"></a>原因

可能不受信任的 HTTP 请求输入达到原始 XML 输出。

## <a name="rule-description"></a>规则说明

使用不受信任的输入时，请注意 XML 注入攻击。 攻击者可以使用 XML 注入向 XML 文档中插入特殊字符，使文档无效 XML。 或者，攻击者可能会恶意地插入其所选的 XML 节点。

此规则尝试从进入原始 XML 写入的 HTTP 请求查找输入。

> [!NOTE]
> 此规则无法跟踪程序集中的数据。 例如，如果一个程序集读取 HTTP 请求输入，然后将其传递给写入原始 XML 的另一个程序集，则此规则不会产生警告。

> [!NOTE]
> 此规则将跨方法调用分析数据流的程度有可配置的限制。 有关如何在 EditorConfig 文件中配置限制的说明，请参阅[分析器配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md#dataflow-analysis)。

## <a name="how-to-fix-violations"></a>如何解决冲突

请勿写入原始 XML。 请改用 XML 编码其输入的方法或属性。

或者，在编写原始 XML 之前对输入进行 XML 编码。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

请勿禁止显示此规则的警告。

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System;
using System.Xml;

public partial class WebForm : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        string input = Request.Form["in"];
        XmlDocument d = new XmlDocument();
        XmlElement root = d.CreateElement("root");
        d.AppendChild(root);

        XmlElement allowedUser = d.CreateElement("allowedUser");
        root.AppendChild(allowedUser);

        allowedUser.InnerXml = "alice";

        // If an attacker uses this for input:
        //     some text<allowedUser>oscar</allowedUser>
        // Then the XML document will be:
        //     <root>some text<allowedUser>oscar</allowedUser></root>
        root.InnerXml = input;
    }
}
```

```vb
Imports System
Imports System.Xml

Public Partial Class WebForm
    Inherits System.Web.UI.Page

    Sub Page_Load(sender As Object, e As EventArgs)
        Dim input As String = Request.Form("in")
        Dim d As XmlDocument = New XmlDocument()
        Dim root As XmlElement = d.CreateElement("root")
        d.AppendChild(root)

        Dim allowedUser As XmlElement = d.CreateElement("allowedUser")
        root.AppendChild(allowedUser)

        allowedUser.InnerXml = "alice"

        ' If an attacker uses this for input:
        '     some text<allowedUser>oscar</allowedUser>
        ' Then the XML document will be:
        '     <root>some text<allowedUser>oscar</allowedUser></root>
        root.InnerXml = input
    End Sub
End Class
```

### <a name="solution"></a>解决方案

```csharp
using System;
using System.Xml;

public partial class WebForm : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        string input = Request.Form["in"];
        XmlDocument d = new XmlDocument();
        XmlElement root = d.CreateElement("root");
        d.AppendChild(root);

        XmlElement allowedUser = d.CreateElement("allowedUser");
        root.AppendChild(allowedUser);

        allowedUser.InnerText = "alice";

        // If an attacker uses this for input:
        //     some text<allowedUser>oscar</allowedUser>
        // Then the XML document will be:
        //     <root>&lt;allowedUser&gt;oscar&lt;/allowedUser&gt;some text<allowedUser>alice</allowedUser></root>
        root.InnerText = input;
    }
}
```

```vb
Imports System
Imports System.Xml

Public Partial Class WebForm
    Inherits System.Web.UI.Page

    Sub Page_Load(sender As Object, e As EventArgs)
        Dim input As String = Request.Form("in")
        Dim d As XmlDocument = New XmlDocument()
        Dim root As XmlElement = d.CreateElement("root")
        d.AppendChild(root)

        Dim allowedUser As XmlElement = d.CreateElement("allowedUser")
        root.AppendChild(allowedUser)

        allowedUser.InnerText = "alice"

        ' If an attacker uses this for input:
        '     some text<allowedUser>oscar</allowedUser>
        ' Then the XML document will be:
        '     <root>&lt;allowedUser&gt;oscar&lt;/allowedUser&gt;some text<allowedUser>alice</allowedUser></root>
        root.InnerText = input
    End Sub
End Class
```
