---
title: CA3008：查看 XPath 注入漏洞的代码
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
ms.openlocfilehash: 5a4b80b8ede1ab2b8d858ed7378f318f2eebe5fa
ms.sourcegitcommit: 2ee11676af4f3fc5729934d52541e9871fb43ee9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65841541"
---
# <a name="ca3008-review-code-for-xpath-injection-vulnerabilities"></a>CA3008：查看 XPath 注入漏洞的代码

|||
|-|-|
|TypeName|ReviewCodeForXPathInjectionVulnerabilities|
|CheckId|CA3008|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

可能不受信任的 HTTP 请求输入达到 XPath 查询。

## <a name="rule-description"></a>规则说明

在使用时不受信任的输入，留意 XPath 注入式攻击。 构造使用不受信任的输入的 XPath 查询可能会允许攻击者恶意操作的查询返回意外的结果，并可能是公开的查询的 XML 内容。

此规则会尝试查找来自 HTTP 请求到达的 XPath 表达式的输入。

> [!NOTE]
> 此规则不能跨程序集跟踪数据。 例如，如果一个程序集读取 HTTP 请求输入，然后将其传递给另一个程序集执行 XPath 查询，此规则不会生成一条警告。

> [!NOTE]
> 没有可配置限制深度此规则将分析数据流，在方法调用之间。 请参阅[分析器的配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md#dataflow-analysis)了解用于某个 EditorConfig 文件中配置限制。

## <a name="how-to-fix-violations"></a>如何解决冲突

修复 XPath 注入漏洞的一些方法包括：

- 不构造从用户输入的 XPath 查询。
- 验证输入只包含一组安全的字符。
- 对引号进行转义。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果您知道已验证的输入为安全起见，则可以禁止显示此警告。

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System;
using System.Xml.XPath;

public partial class WebForm : System.Web.UI.Page
{
    public XPathNavigator AuthorizedOperations { get; set; }

    protected void Page_Load(object sender, EventArgs e)
    {
        string operation = Request.Form["operation"];

        // If an attacker uses this for input:
        //     ' or 'a' = 'a
        // Then the XPath query will be:
        //     authorizedOperation[@username = 'anonymous' and @operationName = '' or 'a' = 'a']
        // and it will return any authorizedOperation node.
        XPathNavigator node = AuthorizedOperations.SelectSingleNode(
            "//authorizedOperation[@username = 'anonymous' and @operationName = '" + operation + "']");
    }
}
```

```vb
Imports System
Imports System.Xml.XPath

Partial Public Class WebForm
    Inherits System.Web.UI.Page

    Public Property AuthorizedOperations As XPathNavigator

    Protected Sub Page_Load(sender As Object, e As EventArgs)
        Dim operation As String = Me.Request.Form("operation")

        ' If an attacker uses this for input:
        '     ' or 'a' = 'a
        ' Then the XPath query will be:
        '      authorizedOperation[@username = 'anonymous' and @operationName = '' or 'a' = 'a']
        ' and it will return any authorizedOperation node.
        Dim node As XPathNavigator = AuthorizedOperations.SelectSingleNode( _
            "//authorizedOperation[@username = 'anonymous' and @operationName = '" + operation + "']")
    End Sub
End Class
```
