---
title: CA3012：查看正则表达式注入漏洞的代码
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
ms.openlocfilehash: b66e28804e85b04b1492a20828c42a9b5efd3cf8
ms.sourcegitcommit: 2ee11676af4f3fc5729934d52541e9871fb43ee9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65841042"
---
# <a name="ca3012-review-code-for-regex-injection-vulnerabilities"></a>CA3012：查看正则表达式注入漏洞的代码

|||
|-|-|
|TypeName|ReviewCodeForRegexInjectionVulnerabilities|
|CheckId|CA3012|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

可能不受信任的 HTTP 请求输入到达正则表达式。

## <a name="rule-description"></a>规则说明

在使用时不受信任的输入，留意的正则表达式注入式攻击。 攻击者可以使用正则表达式注入恶意修改正则表达式，以使正则表达式匹配意外的结果，或使正则表达式使用过多的 CPU，从而导致拒绝服务攻击。

此规则会尝试查找来自 HTTP 请求到达正则表达式的输入。

> [!NOTE]
> 此规则不能跨程序集跟踪数据。 例如，如果一个程序集读取 HTTP 请求输入，然后将其传递给创建正则表达式的另一个程序集，此规则不会生成一条警告。

> [!NOTE]
> 没有可配置限制深度此规则将分析数据流，在方法调用之间。 请参阅[分析器的配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md#dataflow-analysis)了解用于某个 EditorConfig 文件中配置限制。

## <a name="how-to-fix-violations"></a>如何解决冲突

针对正则表达式注入一些缓解措施包括：

- 始终使用[匹配超时](/dotnet/standard/base-types/best-practices#use-time-out-values)时使用正则表达式。
- 避免使用基于用户输入的正则表达式。
- 通过调用从用户输入转义的特殊字符<xref:System.Text.RegularExpressions.Regex.Escape%2A?displayProperty=fullName>或另一种方法。
- 允许从用户输入仅非特殊字符。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果您知道要将[匹配超时](/dotnet/standard/base-types/best-practices#use-time-out-values)和用户输入是免费的特殊字符，可以禁止显示此警告。

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System;
using System.Text.RegularExpressions;

public partial class WebForm : System.Web.UI.Page
{
    public string SearchableText { get; set; }

    protected void Page_Load(object sender, EventArgs e)
    {
        string findTerm = Request.Form["findTerm"];
        Match m = Regex.Match(SearchableText, "^term=" + findTerm);
    }
}
```

```vb
Imports System
Imports System.Text.RegularExpressions

Public Partial Class WebForm
    Inherits System.Web.UI.Page

    Public Property SearchableText As String

    Protected Sub Page_Load(sender As Object, e As EventArgs)
        Dim findTerm As String = Request.Form("findTerm")
        Dim m As Match = Regex.Match(SearchableText, "^term=" + findTerm)
    End Sub
End Class
```
