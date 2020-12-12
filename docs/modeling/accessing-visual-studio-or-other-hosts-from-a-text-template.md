---
title: 从文本模板访问 Visual Studio 或其他主机
description: 了解如何使用文本模板中的方法和属性，该模板由执行模板的主机公开。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4c0f19f96ee5f6879ccc3328c29d0e1fa1d2a6d0
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/12/2020
ms.locfileid: "97362244"
---
# <a name="access-visual-studio-or-other-hosts-from-a-text-template"></a>从文本模板访问 Visual Studio 或其他主机

在文本模板中，可以使用由执行模板的主机公开的方法和属性。 Visual Studio 是主机的一个示例。

> [!NOTE]
> 您可以在常规文本模板中使用主机方法和属性，但不能在 *预处理* 文本模板中使用。

## <a name="obtain-access-to-the-host"></a>获取对主机的访问权限

若要访问宿主，请 `hostspecific="true"` 在指令中设置 `template` 。 现在，可以使用 `this.Host` 类型为 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))的。 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))类型具有可用于解析文件名和日志错误的成员，例如。

### <a name="resolve-file-names"></a>解析文件名

若要查找相对于文本模板的文件的完整路径，请使用 `this.Host.ResolvePath()` 。

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="System.IO" #>
<#
 // Find a path within the same project as the text template:
 string myFile = File.ReadAllText(this.Host.ResolvePath("MyFile.txt"));
#>
Content of myFile is:
<#= myFile #>
```

### <a name="display-error-messages"></a>显示错误消息

此示例在转换模板时记录消息。 如果主机是 Visual Studio，则会将错误添加到 **错误列表**。

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="System.CodeDom.Compiler" #>
<#
  string message = "test message";
  this.Host.LogErrors(new CompilerErrorCollection()
    { new CompilerError(
       this.Host.TemplateFile, // Identify the source of the error.
       0, 0, "0",   // Line, column, error ID.
       message) }); // Message displayed in error window.
#>
```

## <a name="use-the-visual-studio-api"></a>使用 Visual Studio API

如果要在 Visual Studio 中执行文本模板，可以使用 `this.Host` 来访问 Visual studio 提供的服务和加载的任何包或扩展。

将 hostspecific = "true" 并强制转换 `this.Host` 为 <xref:System.IServiceProvider> 。

此示例将 Visual Studio API <xref:EnvDTE.DTE> 作为服务获取：

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ assembly name="EnvDTE" #>
<#@ import namespace="EnvDTE" #>
<#
 IServiceProvider serviceProvider = (IServiceProvider)this.Host;
 DTE dte = serviceProvider.GetService(typeof(DTE)) as DTE;
#>
Number of projects in this solution: <#=  dte.Solution.Projects.Count #>
```

## <a name="use-hostspecific-with-template-inheritance"></a>结合使用 hostSpecific 与模板继承

指定 `hostspecific="trueFromBase"` 是否也使用 `inherits` 特性，以及是否从指定的模板继承 `hostspecific="true"` 。 如果不这样做，可能会收到一条编译器警告，指出该属性 `Host` 已声明两次。
