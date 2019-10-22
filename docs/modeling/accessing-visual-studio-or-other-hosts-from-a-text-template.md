---
title: 从文本模板访问 Visual Studio 或其他主机
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 752b9d9e69eee26f267927f03c4b83c68740100b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652364"
---
# <a name="access-visual-studio-or-other-hosts-from-a-text-template"></a>从文本模板访问 Visual Studio 或其他主机

在文本模板中，可以使用由执行模板的主机公开的方法和属性。 Visual Studio 是主机的一个示例。

> [!NOTE]
> 您可以在常规文本模板中使用主机方法和属性，但不能在*预处理*文本模板中使用。

## <a name="obtain-access-to-the-host"></a>获取对主机的访问权限

若要访问宿主，请在 `template` 指令中设置 `hostspecific="true"`。 现在，可以使用[ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))类型的 `this.Host`。 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))类型具有可用于解析文件名和日志错误的成员，例如。

### <a name="resolve-file-names"></a>解析文件名

若要查找相对于文本模板的文件的完整路径，请使用 `this.Host.ResolvePath()`。

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

此示例在转换模板时记录消息。 如果主机是 Visual Studio，则会将错误添加到**错误列表**。

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

如果要在 Visual Studio 中执行文本模板，可以使用 `this.Host` 来访问 Visual Studio 提供的服务以及所加载的任何包或扩展。

设置 hostspecific = "true"，并将 `this.Host` 转换为 <xref:System.IServiceProvider>。

此示例以服务的形式获取 Visual Studio API <xref:EnvDTE.DTE>：

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

如果还使用 `inherits` 属性，则指定 `hostspecific="trueFromBase"`; 如果从指定 `hostspecific="true"` 的模板继承，则指定。 如果不这样做，可能会收到一条编译器警告，指出已将属性 `Host` 声明了两次。