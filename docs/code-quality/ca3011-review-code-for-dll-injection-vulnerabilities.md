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
ms.openlocfilehash: 4c9fbb4b8b11b0fce7d3e7530eef80af19b35b73
ms.sourcegitcommit: 2ee11676af4f3fc5729934d52541e9871fb43ee9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65841028"
---
# <a name="ca3011-review-code-for-dll-injection-vulnerabilities"></a>CA3011：查看 DLL 注入漏洞的代码

|||
|-|-|
|TypeName|ReviewCodeForDllInjectionVulnerabilities|
|CheckId|CA3011|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

可能不受信任的 HTTP 请求输入达到的一种方法加载程序集。

## <a name="rule-description"></a>规则说明

在使用时不受信任的输入，留意加载不受信任的代码。 如果 web 应用程序加载不受信任的代码，攻击者可能能够将恶意 Dll 注入到你的过程并执行恶意代码。

此规则会尝试查找来自达到加载程序集的方法的 HTTP 请求的输入。

> [!NOTE]
> 此规则不能跨程序集跟踪数据。 例如，如果一个程序集读取 HTTP 请求输入，然后将其传递给加载程序集的另一个程序集，此规则不会生成一条警告。

> [!NOTE]
> 没有可配置限制深度此规则将分析数据流，在方法调用之间。 请参阅[分析器的配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md#dataflow-analysis)了解用于某个 EditorConfig 文件中配置限制。

## <a name="how-to-fix-violations"></a>如何解决冲突

从用户输入不加载不受信任的 Dll。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则的警告。

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
