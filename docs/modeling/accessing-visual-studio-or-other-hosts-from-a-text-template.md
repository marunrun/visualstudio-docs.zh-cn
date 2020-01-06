---
title: 从文本模板访问 Visual Studio 或其他主机
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cd69ae5864df9cbddd204c45975736fc4aae49e5
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75597251"
---
# <a name="access-visual-studio-or-other-hosts-from-a-text-template"></a>从文本模板访问 Visual Studio 或其他主机

在文本模板中，可以使用由主机执行该模板的公开的方法和属性。 Visual Studio 是主机的一个示例。

> [!NOTE]
> 在正则文本模板，但不是在可以使用主机的方法和属性*预处理过的*文本模板。

## <a name="obtain-access-to-the-host"></a>获取对主机的访问

若要访问主机，请设置`hostspecific="true"`在`template`指令。 现在，可以使用[ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))类型的 `this.Host`。 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))类型具有可用于解析文件名和日志错误的成员，例如。

### <a name="resolve-file-names"></a>解析文件名称

若要查找相对于文本模板文件的完整路径，请使用`this.Host.ResolvePath()`。

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

转换模板时，此示例中记录消息。 如果主机是 Visual Studio，将错误添加到**错误列表**。

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

如果您正在 Visual Studio 中执行文本模板，则可以使用`this.Host`访问服务提供的 Visual Studio 和任何包或已加载的扩展。

设置 hostspecific ="true"，并强制转换`this.Host`到<xref:System.IServiceProvider>。

此示例将获取 Visual Studio API， <xref:EnvDTE.DTE>，作为一项服务：

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

## <a name="use-hostspecific-with-template-inheritance"></a>使用模板继承 hostSpecific

指定`hostspecific="trueFromBase"`如果你还使用`inherits`属性，如果指定的模板继承`hostspecific="true"`。 如果不这样做，您可能会获取编译器警告的属性`Host`具有已声明了两次。
