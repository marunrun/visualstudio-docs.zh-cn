---
title: T4 包含指令
ms.date: 11/04/2016
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a1ee58c29be3c4dfb5e2148c54464a7a511d1839
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "75591848"
---
# <a name="t4-include-directive"></a>T4 包含指令

在 Visual Studio 中的文本模板中，可以通过使用指令包含来自其他文件的文本 `<#@include#>` 。 可以将 `include` 指令放置在文本模板中第一个类功能块 `<#+ ... #>` 前面的任何位置。 包含文件还可以包含 `include` 指令和其他指令。 这将允许你在模板之间共享模板代码和样本文本。

## <a name="using-include-directives"></a>使用 Include 指令

```
<#@ include file="filePath" [once="true"] #>
```

- `filePath` 可以是绝对的，也可以是相对于当前模板文件的相对路径。

   此外，特定 Visual Studio 扩展可以指定其自己的目录来搜索包含文件。 例如，在安装了可视化和建模 SDK (DSL 工具) 后，会将以下文件夹添加到包含列表： `Program Files\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft\DSL SDK\DSL Designer\11.0\TextTemplates` 。

   这些附加包含文件夹可能取决于包含文件的文件扩展名。 例如，DSL 工具包含仅具有文件扩展名 `.tt` 的包含文件可访问的文件夹。

- `filePath` 可以包括用“%”分隔的环境变量。 例如：

  ```
  <#@ include file="%HOMEPATH%\MyIncludeFile.t4" #>
  ```

- 包含的文件的名称将不必使用扩展名 `".tt"`。

   你可能需要对包含的文件使用其他扩展名，例如，`".t4"`。 这是因为，当你向 `.tt` 项目添加文件时，Visual Studio 会自动将其 " **自定义工具** " 属性设置为 `TextTemplatingFileGenerator` 。 你通常不希望单独转换包含的文件。

   另一方面，在某种情况下应注意，文件扩展名会影响将要搜索哪些附加文件夹来获得包含文件。 您具有包括其他文件的已包含文件时，这可能会很重要。

- 在处理时，被包含内容就像是包含文本模板的组成部分一样。 不过，即使 `<#+...#>` 指令后为普通文本块和标准控制块，也可以包括含有类功能块 `include` 的文件。

- 用于 `once="true"` 确保模板仅包含一次，即使它是从多个其他包含文件中调用的。

   利用此功能，可以轻松构建可重复使用的 T4 代码库，而不必担心其他一些代码段已经包含它们。  例如，假设您有一个非常精细的代码段库，用于处理模板处理和 c # 生成。  进而，某些特定于任务的实用程序（如生成异常）使用这些工具，然后可以从任何应用程序特定的模板使用它们。 如果绘制依赖项关系图，则你会看到将会多次包含某些代码片段。 但 `once` 参数阻止后续包含。

  **MyTextTemplate.tt：**

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

 **TextFile1.t4：**

```
   Output Message 2 (from included file).
<#@ include file="TextFile2.t4" #>
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

 **TextFile2.t4：**

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

 **得到的已生成文件，MyTextTemplate.txt：**

```
Output message 1 (from top template).
   Output Message 2 (from included file).
        Output Message 3 (from included file 2).

   Output Message 4 (from included file).

Output message 5 (from top template).
   Output Message 6 (from GenerateMessage method).
       Output Message 7 (from AnotherGenerateMessage method).
```

## <a name="using-project-properties-in-msbuild-and-visual-studio"></a><a name="msbuild"></a> 在 MSBuild 和 Visual Studio 中使用项目属性
 尽管可以在 include 指令中使用类似 $ (SolutionDir) 的 Visual Studio 宏，但它们在 MSBuild 中不起作用。 如果你想要在生成计算机中转换模板，则必须改用项目属性。

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
