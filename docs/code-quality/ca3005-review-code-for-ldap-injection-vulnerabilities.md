---
title: CA3005：查看 LDAP 注入漏洞的代码
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
ms.openlocfilehash: 10b9091df08368674511b770158ea47c247aade7
ms.sourcegitcommit: 2ee11676af4f3fc5729934d52541e9871fb43ee9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65841364"
---
# <a name="ca3005-review-code-for-ldap-injection-vulnerabilities"></a>CA3005：查看 LDAP 注入漏洞的代码

|||
|-|-|
|TypeName|ReviewCodeForLdapInjectionVulnerabilities|
|CheckId|CA3005|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

可能不受信任的 HTTP 请求输入达到 LDAP 语句。

## <a name="rule-description"></a>规则说明

在使用时不受信任的输入，留意的轻型目录访问协议 (LDAP) 注入式攻击。 攻击者可以针对信息目录运行恶意 LDAP 语句。 使用用户输入构造动态 LDAP 语句来访问目录服务的应用程序是特别容易受到攻击。

此规则会尝试查找来自 HTTP 请求到达的 LDAP 语句的输入。

> [!NOTE]
> 此规则不能跨程序集跟踪数据。 例如，如果一个程序集读取 HTTP 请求输入，然后将其传递给执行 LDAP 语句的另一个程序集，此规则不会生成一条警告。

> [!NOTE]
> 没有可配置限制深度此规则将分析数据流，在方法调用之间。 请参阅[分析器的配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md#dataflow-analysis)了解用于某个 EditorConfig 文件中配置限制。

## <a name="how-to-fix-violations"></a>如何解决冲突

LDAP 语句的用户控制部分，请考虑之一：
- 允许安全列表的非特殊字符。
- 不允许特殊字符
- 特殊字符进行转义。

请参阅[OWASP 的 LDAP 注入预防速查表](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/LDAP_Injection_Prevention_Cheat_Sheet.md)有关更多指导。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果您知道验证输入或将其转义为安全起见，则可以禁止显示此警告。

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System;
using System.DirectoryServices;

public partial class WebForm : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        string userName = Request.Params["user"];
        string filter = "(uid=" + userName + ")";  // searching for the user entry

        // In this example, if we send the * character in the user parameter which will
        // result in the filter variable in the code to be initialized with (uid=*).
        // The resulting LDAP statement will make the server return any object that
        // contains a uid attribute.
        DirectorySearcher searcher = new DirectorySearcher(filter);
        SearchResultCollection results = searcher.FindAll();

        // Iterate through each SearchResult in the SearchResultCollection.
        foreach (SearchResult searchResult in results)
        {
            // ...
        }
    }
}
```

```vb
Imports System
Imports System.DirectoryServices

Partial Public Class WebForm
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(send As Object, e As EventArgs)
        Dim userName As String = Me.Request.Params(""user"")
        Dim filter As String = ""(uid="" + userName + "")""    ' searching for the user entry

        ' In this example, if we send the * character in the user parameter which will
        ' result in the filter variable in the code to be initialized with (uid=*).
        ' The resulting LDAP statement will make the server return any object that
        ' contains a uid attribute.
        Dim searcher As DirectorySearcher = new DirectorySearcher(filter)
        Dim results As SearchResultCollection = searcher.FindAll()

        ' Iterate through each SearchResult in the SearchResultCollection.
        For Each searchResult As SearchResult in results
            ' ...
        Next searchResult
    End Sub
End Class
```
