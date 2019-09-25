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
ms.openlocfilehash: 42808b3961b18a23f594800f9d0782c908c9b1ba
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71237180"
---
# <a name="ca3012-review-code-for-regex-injection-vulnerabilities"></a>CA3012：查看正则表达式注入漏洞的代码

|||
|-|-|
|TypeName|ReviewCodeForRegexInjectionVulnerabilities|
|CheckId|CA3012|
|类别|Microsoft.Security|
|重大更改|不间断|

## <a name="cause"></a>原因

可能不受信任的 HTTP 请求输入达到正则表达式。

## <a name="rule-description"></a>规则说明

使用不受信任的输入时，请注意 regex 注入式攻击。 攻击者可以使用 regex 注入来恶意地修改正则表达式，以使 regex 与意外结果匹配，或使 regex 消耗过多的 CPU，导致拒绝服务攻击。

此规则尝试从到达正则表达式的 HTTP 请求查找输入。

> [!NOTE]
> 此规则无法跟踪程序集中的数据。 例如，如果一个程序集读取 HTTP 请求输入，然后将其传递给另一个创建正则表达式的程序集，则此规则不会产生警告。

> [!NOTE]
> 此规则将跨方法调用分析数据流的程度有可配置的限制。 有关如何在 EditorConfig 文件中配置限制的说明，请参阅[分析器配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md#dataflow-analysis)。

## <a name="how-to-fix-violations"></a>如何解决冲突

针对 regex 注入的一些缓解措施包括：

- 使用正则表达式时，始终使用[匹配超时](/dotnet/standard/base-types/best-practices#use-time-out-values)。
- 避免使用基于用户输入的正则表达式。
- 通过调用<xref:System.Text.RegularExpressions.Regex.Escape%2A?displayProperty=fullName>或其他方法，从用户输入中转义特殊字符。
- 仅允许来自用户输入的非特殊字符。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果你知道要使用[匹配超时](/dotnet/standard/base-types/best-practices#use-time-out-values)并且用户输入没有特殊字符，则可以禁止显示此警告。

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
