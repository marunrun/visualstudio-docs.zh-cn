---
title: CA3003:查看文件路径注入漏洞的代码
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
ms.openlocfilehash: b81bd810bac142bdec23074e69bbd3840043c8f6
ms.sourcegitcommit: 2ee11676af4f3fc5729934d52541e9871fb43ee9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65841388"
---
# <a name="ca3003-review-code-for-file-path-injection-vulnerabilities"></a>CA3003:查看文件路径注入漏洞的代码

|||
|-|-|
|TypeName|ReviewCodeForFilePathInjectionVulnerabilities|
|CheckId|CA3003|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

可能不受信任的 HTTP 请求输入达到文件操作的路径。

## <a name="rule-description"></a>规则说明

当处理从 web 请求不受信任的输入，留意使用用户控制的输入时指定文件的路径。 攻击者可能能够读取无意的文件，从而导致信息泄露的敏感数据。 或者，攻击者可能能够写入到非预期的文件，从而导致敏感数据的未经授权的修改或影响服务器的安全性。 是一种常用的攻击者技术[路径遍历](https://www.owasp.org/index.php/Path_Traversal)访问位于目标目录之外的文件。

此规则会尝试查找来自 HTTP 请求到达文件操作中的路径的输入。

> [!NOTE]
> 此规则不能跨程序集跟踪数据。 例如，如果一个程序集读取 HTTP 请求输入，然后将其传递给另一个程序集，它将写入到一个文件，此规则不会生成一条警告。

> [!NOTE]
> 没有可配置限制深度此规则将分析数据流，在方法调用之间。 请参阅[分析器的配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md#dataflow-analysis)了解用于某个 EditorConfig 文件中配置限制。

## <a name="how-to-fix-violations"></a>如何解决冲突

- 如果可能，请限制基于用户输入到显式已知的安全列表的文件路径。  例如，如果你的应用程序只需访问"red.txt"、"green.txt"或"blue.txt"，只允许这些值。
- 检查不受信任的文件名，并验证该名称的格式正确。
- 指定路径时，请使用完整路径名称。
- 避免潜在的危险构造，例如路径环境变量。
- 仅接受的长文件名和验证长名称，如果用户提交的短名称。
- 最终用户将输入限制为有效的字符。
- 拒绝其中超过 MAX_PATH 长度的名称。
- 按字面意思进行解释而处理文件名。
- 确定文件名是否表示一个文件或设备。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果验证输入了上一节中所述，，也没关系，若要取消显示此警告。

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System;
using System.IO;

public partial class WebForm : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        string userInput = Request.Params["UserInput"];
        // Assume the following directory structure:
        //   wwwroot\currentWebDirectory\user1.txt
        //   wwwroot\currentWebDirectory\user2.txt
        //   wwwroot\secret\allsecrets.txt
        // There is nothing wrong if the user inputs:
        //   user1.txt
        // However, if the user input is:
        //   ..\secret\allsecrets.txt
        // Then an attacker can now see all the secrets.

        // Avoid this:
        using (File.Open(userInput, FileMode.Open))
        {
            // Read a file with the name supplied by user
            // Input through request's query string and display
            // The content to the webpage.
        }
    }
}
```

```vb
Imports System
Imports System.IO

Partial Public Class WebForm
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(sender As Object, e As EventArgs)
        Dim userInput As String = Me.Request.Params("UserInput")
        ' Assume the following directory structure:
        '   wwwroot\currentWebDirectory\user1.txt
        '   wwwroot\currentWebDirectory\user2.txt
        '   wwwroot\secret\allsecrets.txt
        ' There is nothing wrong if the user inputs:
        '   user1.txt
        ' However, if the user input is:
        '   ..\secret\allsecrets.txt
        ' Then an attacker can now see all the secrets.

        ' Avoid this:
        Using File.Open(userInput, FileMode.Open)
            ' Read a file with the name supplied by user
            ' Input through request's query string and display
            ' The content to the webpage.
        End Using
    End Sub
End Class
```
