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
ms.openlocfilehash: c9e43dcdf1e923cb7bc4a98b17fd0be71b7927eb
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71237400"
---
# <a name="ca3003-review-code-for-file-path-injection-vulnerabilities"></a>CA3003:查看文件路径注入漏洞的代码

|||
|-|-|
|TypeName|ReviewCodeForFilePathInjectionVulnerabilities|
|CheckId|CA3003|
|类别|Microsoft.Security|
|重大更改|不间断|

## <a name="cause"></a>原因

可能不受信任的 HTTP 请求输入到达文件操作的路径。

## <a name="rule-description"></a>规则说明

当处理 web 请求中的不受信任输入时，请注意在指定文件路径时使用用户控制输入。 攻击者可能能够读取意外的文件，从而导致信息泄露敏感数据。 或者，攻击者可能能够写入意外的文件，从而导致未经授权的敏感数据修改或危及服务器的安全。 常见的攻击者方法[是访问目标目录](https://www.owasp.org/index.php/Path_Traversal)之外的文件。

此规则尝试从在文件操作中到达路径的 HTTP 请求查找输入。

> [!NOTE]
> 此规则无法跟踪程序集中的数据。 例如，如果一个程序集读取 HTTP 请求输入，然后将其传递给另一个写入文件的程序集，则此规则不会产生警告。

> [!NOTE]
> 此规则将跨方法调用分析数据流的程度有可配置的限制。 有关如何在 EditorConfig 文件中配置限制的说明，请参阅[分析器配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md#dataflow-analysis)。

## <a name="how-to-fix-violations"></a>如何解决冲突

- 如果可能，将基于用户输入的文件路径限制为显式已知的安全列表。  例如，如果应用程序只需访问 "red .txt"、"绿 .txt" 或 "blue .txt"，则只允许使用这些值。
- 检查不受信任的文件名，并验证名称格式是否正确。
- 指定路径时使用完整路径名称。
- 避免潜在的危险构造，如路径环境变量。
- 如果用户提交短名称，则只接受长文件名并验证长名称。
- 将最终用户输入限制为有效字符。
- 拒绝超过 MAX_PATH 长度的名称。
- 按原义处理文件名，无需解释。
- 确定 filename 是否表示文件或设备。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果已按照上一部分中所述验证输入，则可以禁止显示此警告。

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
