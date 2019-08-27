---
title: 从文本模板访问 Visual Studio 2015 或其他主机 |Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: a68886da-7416-4785-8145-3796bb382cba
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 053e8b09fd2b52683238f1ffe008e5e7d38b3962
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68872010"
---
# <a name="accessing-visual-studio-or-other-hosts-from-a-text-template"></a>从文本模板访问 Visual Studio 或其他主机
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在文本模板中, 可以使用由执行模板的主机公开的方法和属性, 如[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。

 这适用于常规文本模板, 而不是预处理文本模板。

## <a name="obtaining-access-to-the-host"></a>获取对主机的访问权限

在指令中设置`hostspecific="true"` `template` 。 这使你可以`this.Host`使用类型为[ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))的。 此类型具有可以使用的成员, 例如, 解析文件名和记录错误。

### <a name="resolving-file-names"></a>解析文件名
 若要查找相对于文本模板的文件的完整路径, 请使用此方法。ResolvePath ()。

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
 转换模板时，此示例中记录消息。 如果主机是[!INCLUDE[vsprvs](../includes/vsprvs-md.md)], 则会将其添加到错误窗口中。

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
 如果要在中[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]执行文本模板, 则可以使用`this.Host`访问所提供的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]服务以及所加载的任何包或扩展。

 设置 hostspecific ="true"，并强制转换`this.Host`到<xref:System.IServiceProvider>。

 此示例将[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] <xref:EnvDTE.DTE>API 作为服务获取:

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
 指定`hostspecific="trueFromBase"`如果你还使用`inherits`属性，如果指定的模板继承`hostspecific="true"`。 这可以避免编译器警告, 因为该属性`Host`已声明了两次。
