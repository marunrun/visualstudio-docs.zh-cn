---
title: CA3011：查看 DLL 注入漏洞的代码
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
ms.openlocfilehash: a459be8c8ab028581c850f5b5770a95cb70e3510
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71237196"
---
# <a name="ca3011-review-code-for-dll-injection-vulnerabilities"></a>CA3011：查看 DLL 注入漏洞的代码

|||
|-|-|
|TypeName|ReviewCodeForDllInjectionVulnerabilities|
|CheckId|CA3011|
|类别|Microsoft.Security|
|重大更改|不间断|

## <a name="cause"></a>原因

可能不受信任的 HTTP 请求输入将进入加载程序集的方法。

## <a name="rule-description"></a>规则说明

使用不受信任的输入时，请注意加载不受信任的代码。 如果你的 web 应用程序加载不受信任的代码，攻击者可能能够将恶意 Dll 注入到你的进程中并执行恶意代码。

此规则尝试从 HTTP 请求查找输入，该请求将到达加载程序集的方法。

> [!NOTE]
> 此规则无法跟踪程序集中的数据。 例如，如果一个程序集读取 HTTP 请求输入，然后将其传递给加载程序集的另一个程序集，则此规则不会产生警告。

> [!NOTE]
> 此规则将跨方法调用分析数据流的程度有可配置的限制。 有关如何在 EditorConfig 文件中配置限制的说明，请参阅[分析器配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md#dataflow-analysis)。

## <a name="how-to-fix-violations"></a>如何解决冲突

不要从用户输入中加载不受信任的 Dll。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

请勿禁止显示此规则的警告。

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System;
using System.Reflection;

public partial class WebForm : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        string input = Request.Form["in"];
        byte[] rawAssembly = Convert.FromBase64String(input);
        Assembly.Load(rawAssembly);
    }
}
```

```vb
Imports System
Imports System.Reflection

Public Partial Class WebForm
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(sender As Object, e As EventArgs)
        Dim input As String = Request.Form("in")
        Dim rawAssembly As Byte() = Convert.FromBase64String(input)
        Assembly.Load(rawAssembly)
    End Sub
End Class
```
