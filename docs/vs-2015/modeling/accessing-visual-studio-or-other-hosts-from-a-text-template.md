---
title: 从文本模板访问 Visual Studio 2015 或其他主机 |Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: a68886da-7416-4785-8145-3796bb382cba
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0e8cedc66d6b52f80239364a3e51b73e93a69aa4
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655324"
---
# <a name="accessing-visual-studio-or-other-hosts-from-a-text-template"></a>从文本模板访问 Visual Studio 或其他主机
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在文本模板中，可以使用由执行模板的主机公开的方法和属性，如 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。

 这适用于常规文本模板，而不是预处理文本模板。

## <a name="obtaining-access-to-the-host"></a>获取对主机的访问权限

在 `template` 指令中设置 `hostspecific="true"`。 这使你可以使用[ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))类型的 `this.Host`。 此类型具有可以使用的成员，例如，解析文件名和记录错误。

### <a name="resolving-file-names"></a>解析文件名
 若要查找相对于文本模板的文件的完整路径，请使用此方法。ResolvePath （）。

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

### <a name="displaying-error-messages"></a>显示错误消息
 此示例在转换模板时记录消息。 如果主机是 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的，则会将其添加到错误窗口中。

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

## <a name="using-the-visual-studio-api"></a>使用 Visual Studio API
 如果要在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中执行文本模板，则可以使用 `this.Host` 来访问 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 和所加载的任何包或扩展所提供的服务。

 设置 hostspecific = "true"，并将 `this.Host` 转换为 <xref:System.IServiceProvider>。

 此示例以服务的形式获取 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] API <xref:EnvDTE.DTE>：

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

## <a name="using-hostspecific-with-template-inheritance"></a>将 hostSpecific 与模板继承一起使用
 如果还使用 `inherits` 属性，则指定 `hostspecific="trueFromBase"`; 如果从指定 `hostspecific="true"` 的模板继承，则指定。 这可以避免编译器警告，因为属性 `Host` 已声明了两次。
