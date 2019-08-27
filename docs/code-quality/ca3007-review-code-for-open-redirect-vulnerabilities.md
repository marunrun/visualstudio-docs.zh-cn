---
title: CA3007：查看公开重定向漏洞的代码
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
ms.openlocfilehash: e60d0fad1262138b57f079485bc7455e55c7ec25
ms.sourcegitcommit: 2ee11676af4f3fc5729934d52541e9871fb43ee9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65841335"
---
# <a name="ca3007-review-code-for-open-redirect-vulnerabilities"></a>CA3007：查看公开重定向漏洞的代码

|||
|-|-|
|TypeName|ReviewCodeForOpenRedirectVulnerabilities|
|CheckId|CA3007|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

可能不受信任的 HTTP 请求输入可能会达到的 HTTP 响应重定向。

## <a name="rule-description"></a>规则说明

在使用时不受信任的输入，留意打开重定向漏洞。 攻击者可以利用开放重定向漏洞，使用你的网站提供外观是合法的 URL，但重定向到网络钓鱼网站或其他恶意网页戒心访问者。

此规则会尝试查找与到达 HTTP 重定向 URL 的 HTTP 请求的输入。

> [!NOTE]
> 此规则不能跨程序集跟踪数据。 例如，如果一个程序集读取 HTTP 请求输入，然后将其传递给另一个程序集使用的 HTTP 重定向响应，此规则不会生成一条警告。

> [!NOTE]
> 没有可配置限制深度此规则将分析数据流，在方法调用之间。 请参阅[分析器的配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md#dataflow-analysis)了解用于某个 EditorConfig 文件中配置限制。

## <a name="how-to-fix-violations"></a>如何解决冲突

修复打开重定向漏洞的一些方法包括：

- 不允许用户启动重定向。
- 不允许用户重定向方案中指定的 URL 的任何部分。
- 限制对预定义"允许列表"的 Url 重定向。
- 验证重定向 Url。
- 如果适用，请考虑使用免责声明页，当用户被重定向离开你的站点。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果您知道在验证了要被限制为预期的 Url 的输入，也没关系，若要取消显示此警告。

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System;

public partial class WebForm : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        string input = Request.Form["url"];
        this.Response.Redirect(input);
    }
}
```

```vb
Imports System

Partial Public Class WebForm
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(sender As Object, eventArgs As EventArgs)
        Dim input As String = Me.Request.Form("url")
        Me.Response.Redirect(input)
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
        if (String.IsNullOrWhiteSpace(input))
        {
            this.Response.Redirect("https://example.org/login.html");
        }
    }
}
```

```vb
Imports System

Partial Public Class WebForm
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(sender As Object, eventArgs As EventArgs)
        Dim input As String = Me.Request.Form("in")
        If String.IsNullOrWhiteSpace(input) Then
            Me.Response.Redirect("https://example.org/login.html")
        End If
    End Sub
End Class
```
