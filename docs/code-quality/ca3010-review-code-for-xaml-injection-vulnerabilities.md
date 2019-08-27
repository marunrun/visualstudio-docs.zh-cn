---
title: CA3010：查看 XAML 注入漏洞的代码
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
ms.openlocfilehash: 965e0d800bd7c725236d96499d2bf2d441b40412
ms.sourcegitcommit: 2ee11676af4f3fc5729934d52541e9871fb43ee9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65841093"
---
# <a name="ca3010-review-code-for-xaml-injection-vulnerabilities"></a>CA3010：查看 XAML 注入漏洞的代码

|||
|-|-|
|TypeName|ReviewCodeForXamlInjectionVulnerabilities|
|CheckId|CA3010|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

可能不受信任的 HTTP 请求输入达到<xref:System.Windows.Markup.XamlReader?displayProperty=nameWithType>负载方法。

## <a name="rule-description"></a>规则说明

在使用时不受信任的输入，留意 XAML 注入式攻击。 XAML 是一种直接表示对象实例化和执行的标记语言。 这意味着在 XAML 中创建的元素可以与系统资源 （例如，网络访问和文件系统 IO） 进行交互。 如果攻击者可以控制的输入<xref:System.Windows.Markup.XamlReader?displayProperty=nameWithType>加载方法调用中，则攻击者可以执行代码。

此规则会尝试查找达到从 HTTP 请求的输入<xref:System.Windows.Markup.XamlReader?displayProperty=nameWithType>负载方法。

> [!NOTE]
> 此规则不能跨程序集跟踪数据。 例如，如果一个程序集读取 HTTP 请求输入，然后将其传递给加载 XAML 的另一个程序集，此规则不会生成一条警告。

> [!NOTE]
> 没有可配置限制深度此规则将分析数据流，在方法调用之间。 请参阅[分析器的配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md#dataflow-analysis)了解用于某个 EditorConfig 文件中配置限制。

## <a name="how-to-fix-violations"></a>如何解决冲突

不会加载不受信任的 XAML。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则的警告。

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System;
using System.IO;

public partial class WebForm : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        string input = Request.Form["in"];
        byte[] bytes = Convert.FromBase64String(input);
        MemoryStream ms = new MemoryStream(bytes);
        System.Windows.Markup.XamlReader.Load(ms);
    }
}
```

```vb
Imports System
Imports System.IO

Public Partial Class WebForm
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(sender As Object, e As EventArgs)
        Dim input As String = Request.Form("in")
        Dim bytes As Byte() = Convert.FromBase64String(input)
        Dim ms As MemoryStream = New MemoryStream(bytes)
        System.Windows.Markup.XamlReader.Load(ms)
    End Sub
End Class
```
