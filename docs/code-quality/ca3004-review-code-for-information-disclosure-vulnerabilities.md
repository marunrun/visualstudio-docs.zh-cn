---
title: CA3004：查看信息泄露漏洞的代码
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
ms.openlocfilehash: 8e8c8c58a01b9527df472907c8b55a9d175dd91d
ms.sourcegitcommit: 2ee11676af4f3fc5729934d52541e9871fb43ee9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65841615"
---
# <a name="ca3004-review-code-for-information-disclosure-vulnerabilities"></a>CA3004：查看信息泄露漏洞的代码

|||
|-|-|
|TypeName|ReviewCodeForInformationDisclosureVulnerabilities|
|CheckId|CA3004|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

异常的消息、 堆栈跟踪或字符串表示形式可能会达到 web 输出。

## <a name="rule-description"></a>规则说明

泄漏异常信息提供深入的应用程序，这可帮助攻击者内部查找其他漏洞利用的攻击者。

此规则将尝试查找异常消息、 堆栈跟踪或对 HTTP 响应输出的字符串表示形式。

> [!NOTE]
> 此规则不能跨程序集跟踪数据。 例如，如果一个程序集捕获异常，然后将其传递给输出异常的另一个程序集，此规则不会生成一条警告。

> [!NOTE]
> 没有可配置限制深度此规则将分析数据流，在方法调用之间。 请参阅[分析器的配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md#dataflow-analysis)了解用于某个 EditorConfig 文件中配置限制。

## <a name="how-to-fix-violations"></a>如何解决冲突

不输出到 HTTP 响应的异常信息。 相反，提供常规错误消息。 请参阅[OWASP 的错误处理页](https://www.owasp.org/index.php/Error_Handling)有关更多指导。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果你知道应用程序的信任边界内 web 输出，永远不会公开之外，它是可以禁止显示此警告。 这并不常见。 考虑到应用程序的信任边界和数据流可能会随时间变化的。

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System;

public partial class WebForm : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs eventArgs)
    {
        try
        {
            object o = null;
            o.ToString();
        }
        catch (Exception e)
        {
            this.Response.Write(e.ToString());
        }
    }
}
```

```vb
Imports System

Partial Public Class WebForm
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(sender As Object, eventArgs As EventArgs)
        Try
            Dim o As Object = Nothing
            o.ToString()
        Catch e As Exception
            Me.Response.Write(e.ToString())
        End Try
    End Sub
End Class
```

### <a name="solution"></a>解决方案

```csharp
using System;

public partial class WebForm : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs eventArgs)
    {
        try
        {
            object o = null;
            o.ToString();
        }
        catch (Exception e)
        {
            this.Response.Write("An error occurred. Please try again later.");
        }
    }
}
```

```vb
Imports System

Partial Public Class WebForm
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(sender As Object, eventArgs As EventArgs)
        Try
            Dim o As Object = Nothing
            o.ToString()
        Catch e As Exception
            Me.Response.Write("An error occurred. Please try again later.")
        End Try
    End Sub
End Class
```