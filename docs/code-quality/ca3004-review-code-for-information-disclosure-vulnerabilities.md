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
ms.openlocfilehash: 4965c9df3c2256511b8e44de8d388a9155d0d8f9
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71237378"
---
# <a name="ca3004-review-code-for-information-disclosure-vulnerabilities"></a>CA3004：查看信息泄露漏洞的代码

|||
|-|-|
|TypeName|ReviewCodeForInformationDisclosureVulnerabilities|
|CheckId|CA3004|
|类别|Microsoft.Security|
|重大更改|不间断|

## <a name="cause"></a>原因

异常的消息、堆栈跟踪或字符串表示形式达到 web 输出。

## <a name="rule-description"></a>规则说明

泄露异常信息可让攻击者深入了解应用程序的内部机制，从而帮助攻击者找到其他漏洞来利用这些漏洞。

此规则尝试查找异常消息、堆栈跟踪或输出到 HTTP 响应的字符串表示形式。

> [!NOTE]
> 此规则无法跟踪程序集中的数据。 例如，如果一个程序集捕获一个异常，然后将其传递给输出该异常的另一个程序集，则此规则不会产生警告。

> [!NOTE]
> 此规则将跨方法调用分析数据流的程度有可配置的限制。 有关如何在 EditorConfig 文件中配置限制的说明，请参阅[分析器配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md#dataflow-analysis)。

## <a name="how-to-fix-violations"></a>如何解决冲突

不要将异常信息输出到 HTTP 响应。 相反，请提供一般的错误消息。 有关更多指导，请参阅[OWASP 的错误处理页](https://www.owasp.org/index.php/Error_Handling)。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果你知道 web 输出位于应用程序的信任边界内，并且从未在外部公开，则可以禁止显示此警告。 这种情况很少发生。 请注意，应用程序的信任边界和数据流可能会随时间而改变。

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