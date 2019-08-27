---
title: CA3006：查看进程命令注入漏洞的代码
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
ms.openlocfilehash: 35e41301dcf0a1358b6d063ce557212915b5f591
ms.sourcegitcommit: 2ee11676af4f3fc5729934d52541e9871fb43ee9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65841447"
---
# <a name="ca3006-review-code-for-process-command-injection-vulnerabilities"></a>CA3006：查看进程命令注入漏洞的代码

|||
|-|-|
|TypeName|ReviewCodeForProcessCommandInjectionVulnerabilities|
|CheckId|CA3006|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

可能不受信任的 HTTP 请求输入达到处理命令。

## <a name="rule-description"></a>规则说明

在使用时不受信任的输入，留意命令注入式攻击。 命令注入攻击可以基础操作系统，牺牲安全性和完整性的你的服务器上执行恶意命令。

此规则会尝试查找来自 HTTP 请求到达处理命令的输入。

> [!NOTE]
> 此规则不能跨程序集跟踪数据。 例如，如果一个程序集读取 HTTP 请求输入，然后将其传递给另一个程序集，将启动一个进程，此规则不会生成一条警告。

> [!NOTE]
> 没有可配置限制深度此规则将分析数据流，在方法调用之间。 请参阅[分析器的配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md#dataflow-analysis)了解用于某个 EditorConfig 文件中配置限制。

## <a name="how-to-fix-violations"></a>如何解决冲突

- 如果可能，避免在启动时根据用户输入的进程。
- 验证输入针对一组已知安全的字符和长度。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果您知道验证输入或将其转义为安全起见，则可以安全地禁止显示此警告。

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System;
using System.Diagnostics;

public partial class WebForm : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        string input = Request.Form["in"];
        Process p = Process.Start(input);
    }
}
```

```vb
Imports System
Imports System.Diagnostics

Partial Public Class WebForm
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(sender As Object, eventArgs as EventArgs)
        Dim input As String = Me.Request.Form("in")
        Dim p As Process = Process.Start(input)
    End Sub
End Class
```
