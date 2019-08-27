---
title: T4 包含指令 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 8c3de9f3-755a-47c5-a30a-65717dcaaac2
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 6b475b8e5c2138c909133aee0440f0dcaea99e13
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68163643"
---
# <a name="t4-include-directive"></a>T4 包含指令
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的文本模板中，通过使用 `<#@include#>` 指令可包括来自另一个文件的文本。 可以将 `include` 指令放置在文本模板中第一个类功能块 `<#+ ... #>` 前面的任何位置。 包含文件还可以包含 `include` 指令和其他指令。 这将允许你在模板之间共享模板代码和样本文本。  
  
## <a name="using-include-directives"></a>使用 Include 指令  
  
```  
<#@ include file="filePath" [once="true"] #>  
```  
  
- `filePath` 可以是绝对的，或相对于当前模板文件。  
  
   另外，特定 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展可以指定其自己的目录以便搜索包含文件。 例如，当安装了可视化和建模 SDK （DSL 工具），则以下文件夹添加到 include 列表： `Program Files\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft\DSL SDK\DSL Designer\11.0\TextTemplates`。  
  
   这些附加包含文件夹可能取决于包含文件的文件扩展名。 例如，DSL 工具包含仅具有文件扩展名 `.tt` 的包含文件可访问的文件夹。  
  
- `filePath` 可以包括用“%”分隔的环境变量。 例如:  
  
  ```  
  <#@ include file="%HOMEPATH%\MyIncludeFile.t4" #>  
  ```  
  
- 包含的文件的名称将不必使用扩展名 `".tt"`。  
  
   你可能需要对包含的文件使用其他扩展名，例如，`".t4"`。 这是因为，当您将添加`.tt`文件到项目中，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]会自动设置其**自定义工具**属性设置为`TextTemplatingFileGenerator`。 你通常不希望单独转换包含的文件。  
  
   另一方面，在某种情况下应注意，文件扩展名会影响将要搜索哪些附加文件夹来获得包含文件。 您具有包括其他文件的已包含文件时，这可能会很重要。  
  
- 在处理时，被包含内容就像是包含文本模板的组成部分一样。 不过，即使 `<#+...#>` 指令后为普通文本块和标准控制块，也可以包括含有类功能块 `include` 的文件。  
  
- 使用 `once="true"` 以确保一个模板只包括一次，即使从多个其他包括文件对其进行调用也是如此。  
  
   无需担心，我们可以很容易建立一种可重用的 T4 代码段库，可以包括在将此功能使某些其他代码段具有已包括它们。  例如，假设您有非常精准处理模板处理和 C# 生成的代码片段的库。  反过来，这些使用一些更特定于任务的实用程序，例如生成异常，然后，可以使用从任何更多特定于应用程序模板。 如果绘制依赖项关系图，则你会看到将会多次包含某些代码片段。 但 `once` 参数阻止后续包含。  
  
  **MyTextTemplate.tt:**  
  
```  
<#@ output extension=".txt" #>  
Output message 1 (from top template).  
<#@ include file="TextFile1.t4"#>  
Output message 5 (from top template).  
<#  
   GenerateMessage(6); // defined in TextFile1.t4  
   AnotherGenerateMessage(7); // defined in TextFile2.t4  
#>  
  
```  
  
 **TextFile1.t4:**  
  
```  
   Output Message 2 (from included file).  
<#@include file="TextFile2.t4" #>  
   Output Message 4 (from included file).  
<#+ // Start of class feature control block.  
void GenerateMessage(int n)  
{  
#>  
   Output Message <#= n #> (from GenerateMessage method).  
<#+  
}  
#>  
  
```  
  
 **TextFile2.t4:**  
  
```  
        Output Message 3 (from included file 2).  
<#+ // Start of class feature control block.  
void AnotherGenerateMessage(int n)  
{  
#>  
       Output Message <#= n #> (from AnotherGenerateMessage method).  
<#+  
}  
#>  
  
```  
  
 **生成生成文件，MyTextTemplate.txt:**  
  
```  
Output message 1 (from top template).  
   Output Message 2 (from included file).  
        Output Message 3 (from included file 2).  
  
   Output Message 4 (from included file).  
  
Output message 5 (from top template).  
   Output Message 6 (from GenerateMessage method).  
       Output Message 7 (from AnotherGenerateMessage method).  
  
```  
  
## <a name="msbuild"></a> 使用 MSBuild 和 Visual Studio 中的项目属性  
 虽然你可在 Include 指令中使用 Visual Studio 宏（如 $(SolutionDir），但它们在 MSBuild 中不起作用。 如果你想要在生成计算机中转换模板，则必须改用项目属性。  
  
 编辑 .csproj 或 .vbproj 文件以定义项目属性。 此示例定义一个名为 `myIncludeFolder` 的属性：  
  
```xml  
<!-- Define a project property, myIncludeFolder: -->  
<PropertyGroup>  
    <myIncludeFolder>$(MSBuildProjectDirectory)\..\libs</myIncludeFolder>  
</PropertyGroup>  
  
<!-- Tell the MSBuild T4 task to make the property available: -->  
<ItemGroup>  
    <T4ParameterValues Include="myIncludeFolder">  
      <Value>$(myIncludeFolder)</Value>  
    </T4ParameterValues>  
  </ItemGroup>  
  
```  
  
 现在你可在文本模板中使用项目属性，此类模板将在 Visual Studio 和 MSBuild 中正确转换：  
  
```  
<#@ include file="$(myIncludeFolder)\defs.tt" #>  
```
