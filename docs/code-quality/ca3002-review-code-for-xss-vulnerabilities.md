---
title: CA3002：查看 XSS 漏洞的代码
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
ms.openlocfilehash: 383011e53b14ec2cc7dd7474cd050f05295a2a73
ms.sourcegitcommit: 2ee11676af4f3fc5729934d52541e9871fb43ee9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65841467"
---
# <a name="ca3002-review-code-for-xss-vulnerabilities"></a>CA3002：查看 XSS 漏洞的代码

|||
|-|-|
|TypeName|ReviewCodeForXssVulnerabilities|
|CheckId|CA3002|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

可能不受信任的 HTTP 请求输入可能会达到原始 HTML 输出。

## <a name="rule-description"></a>规则说明

当处理从 web 请求不受信任的输入，留意跨站点脚本 (XSS) 攻击。 XSS 攻击注入原始 HTML 输出，从而允许攻击者可以执行恶意脚本或恶意修改您的网页中的内容不受信任的输入。 典型的技巧将置于`<script>`元素与输入中的恶意代码。 有关详细信息，请参阅[OWASP 的 XSS](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS))。

此规则会尝试查找达到原始 HTML 输出的 HTTP 请求中的输入。

> [!NOTE]
> 此规则不能跨程序集跟踪数据。 例如，如果一个程序集读取 HTTP 请求输入，然后将其传递给输出原始 HTML 的另一个程序集，此规则不会生成一条警告。

> [!NOTE]
> 没有可配置限制深度此规则将分析数据流，在方法调用之间。 请参阅[分析器的配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md#dataflow-analysis)了解用于某个 EditorConfig 文件中配置限制。

## <a name="how-to-fix-violations"></a>如何解决冲突

- 而不是输出原始 HTML，使用方法或属性的第一个进行 HTML 编码其输入。
- 不受信任的 HTML 编码前将原始 HTML 输出数据。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

则可以安全地禁止显示此规则的警告，如果：
- 您知道输入进行验证一组已知安全的字符不包含 HTML。
- 您知道的数据经过 HTML 编码中未检测到此规则的一种方法。

> [!NOTE]
> 此规则可能会产生误报的某些方法或属性的 HTML 编码其输入。

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System;

public partial class WebForm : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        string input = Request.Form["in"];
        Response.Write("<HTML>" + input + "</HTML>");
    }
}
```

```vb
Imports System

Partial Public Class WebForm
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(sender As Object, e As EventArgs)
        Dim input As String = Me.Request.Form("in")
        Me.Response.Write("<HTML>" + input + "</HTML>")
    End Sub
End Class
```

### <a name="solution"></a>解决方案

```csharp
using System;

public partial class WebForm : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        string input = Request.Form["in"];

        // Example usage of System.Web.HttpServerUtility.HtmlEncode().
        Response.Write("<HTML>" + Server.HtmlEncode(input) + "</HTML>");
    }
}
```

```vb
Imports System

Partial Public Class WebForm
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(sender As Object, e As EventArgs)
        Dim input As String = Me.Request.Form("in")

        ' Example usage of System.Web.HttpServerUtility.HtmlEncode().
        Me.Response.Write("<HTML>" + Me.Server.HtmlEncode(input) + "</HTML>")
    End Sub
End Class
```