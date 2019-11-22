---
title: Writing a T4 Text Template | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, syntax
- text templates, guide
- text templates, functions that generate text
ms.assetid: 94328da7-953b-4e92-9587-648543d1f732
caps.latest.revision: 45
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: bcd5a4996db4a5e374baabe4f52d5fd1dbac2e5e
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301120"
---
# <a name="writing-a-t4-text-template"></a>编写 T4 文本模板
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

文本模板包含将从其生成的文本。 For example, a template that creates a web page will contain "\<html>…" and all the other standard parts of an HTML page. Inserted into the template are *control blocks*, which are fragments of program code. 控制块提供变化值，允许文本部件是条件和重复的。

 使用这一结构很容易开发模板，因为可以以生成文件为原型，然后逐步插入用于改变结果的控制块。

 文本模板由以下部件组成：

- **Directives** - elements that control how the template is processed.

- **Text blocks** - content that is copied directly to the output.

- **Control blocks** - program code that inserts variable values into the text, and controls conditional or repeated parts of the text.

  To try the examples in this topic, copy them into a template file as described in [Design-Time Code Generation by using T4 Text Templates](../modeling/design-time-code-generation-by-using-t4-text-templates.md). After editing the template file, save it, and then inspect the output **.txt** file.

## <a name="directives"></a>指令
 文本模板指令向文本模板化引擎提供关于如何生成转换代码和输出文件的一般指令。

 例如，下面的指令指定输出文件应具有 .txt 扩展名：

```

<#@ output extension=".txt" #>
```

 For more information about directives, see [T4 Text Template Directives](../modeling/t4-text-template-directives.md).

## <a name="text-blocks"></a>文本块
 文本块直接向输出文件插入文本。 文本块没有特殊格式。 例如，下面的文本模板将生成一个包含单词“Hello”的文本文件：

```
<#@ output extension=".txt" #>
Hello
```

## <a name="control-blocks"></a>控制块
 控制块是用于转换模板的程序代码节。 默认语言是 C#，但若要使用 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]，可以在文件开头编写以下指令：

```
<#@ template language="VB" #>
```

 用于编写控制块代码的语言与生成的文本的语言无关。

### <a name="standard-control-blocks"></a>标准控制块
 标准控制块是生成输出文件部件的程序代码节。

 在模板文件中，可以混合使用任意数量的文本块和标准控制块。 但是，不能在控制块中嵌套控制块。 每个标准控制块都以 `<# ... #>` 符号分隔。

 例如，如果使用下面的控制块和文本块，则输出文件包含行“0, 1, 2, 3, 4 Hello!”：

```

      <#
    for(int i = 0; i < 4; i++)
    {
        Write(i + ", ");
    }
    Write("4");
#> Hello!
```

 你可以交错文本和代码，而不必使用显式 `Write()` 语句。 The following example prints "Hello!" four times:

```
<#
    for(int i = 0; i < 4; i++)
    {
#>
Hello!
<#
    }
#>
```

 在代码中，可以使用 `Write();` 语句的位置都可以插入文本块。

> [!NOTE]
> When you embed a text block within a compound statement such as a loop or conditional, always use braces {...} to contain the text block.

### <a name="expression-control-blocks"></a>表达式控制块
 表达式控制块计算表达式并将其转换为字符串。 该字符串将插入到输出文件中。

 表达式控制块以 `<#= ... #>` 符号分隔。

 例如，如果使用下面的控制块，则输出文件包含“5”：

```
<#= 2 + 3 #>
```

 Notice that the opening symbol has three characters "<#=".

 表达式可以包含作用域中的任何变量。 例如，下面的块输出数字行：

```
<#@ output extension=".txt" #>
<#
    for(int i = 0; i < 4; i++)
    {
#>
This is hello number <#= i+1 #>: Hello!
<#
    }
#>
```

### <a name="class-feature-control-blocks"></a>类功能控制块
 类功能控制块定义属性、方法或不应包含在主转换中的所有其他代码。 类功能块常用于编写帮助器函数。  Typically, class feature blocks are placed in separate files so that they can be [included](#Include) by more than one text template.

 类功能控制块以 `<#+ ... #>` 符号分隔。

 例如，下面的模板文件声明并使用一个方法：

```
<#@ output extension=".txt" #>
Squares:
<#
    for(int i = 0; i < 4; i++)
    {
#>
    The square of <#= i #> is <#= Square(i+1) #>.
<#
    }
#>
That is the end of the list.
<#+   // Start of class feature block
private int Square(int i)
{
    return i*i;
}
#>
```

 类功能必须编写在文件末尾。 不过，即使 `<#@include#>` 指令后跟标准块和文本，也可以 `include` 包含类功能的文件。

 For more information about control blocks, see [Text Template Control Blocks](../modeling/text-template-control-blocks.md).

### <a name="class-feature-blocks-can-contain-text-blocks"></a>类功能块可以包含文本块
 可以编写生成文本的方法。 例如:

```
List of Squares:
<#
   for(int i = 0; i < 4; i++)
   {  WriteSquareLine(i); }
#>
End of list.
<#+   // Class feature block
private void WriteSquareLine(int i)
{
#>
   The square of <#= i #> is <#= i*i #>.
<#+
}
#>
```

 将文本生成方法放置在可供多个模板包含的单独文件中，是非常有用的。

## <a name="using-external-definitions"></a>使用外部定义

### <a name="assemblies"></a>程序集
 模板的代码块可以使用定义了最常用 .NET 程序集（如 System.dll）的类型。 此外，也可以引用其他 .NET 程序集或你自己的程序集。 你可以提供程序集的路径或强名称：

```
<#@ assembly name="System.Xml" #>
```

 应该使用绝对路径名，或在路径名中使用标准宏名。 例如:

```
<#@ assembly name="$(SolutionDir)library\MyAssembly.dll" #>
```

 For a list of macros, see [Common Macros for Build Commands and Properties](https://msdn.microsoft.com/library/239bd708-2ea9-4687-b264-043f1febf98b).

 The assembly directive has no effect in a [preprocessed text template](../modeling/run-time-text-generation-with-t4-text-templates.md).

 For more information, see [T4 Assembly Directive](../modeling/t4-assembly-directive.md).

### <a name="namespaces"></a>命名空间
 import 指令与 C# 中的 `using` 子句或 Visual Basic 中的 `imports` 子句相同。 通过该指令，不使用完全限定名就可以在代码中引用类型：

```
<#@ import namespace="System.Xml" #>
```

 可以根据需要使用任意多个 `assembly` 和 `import` 指令。 必须将它们放在文本块和控制块之前。

 For more information, see [T4 Import Directive](../modeling/t4-import-directive.md).

### <a name="Include"></a> Including code and text
 `include` 指令插入其他模板文件的文本。 例如，下面的指令插入 `test.txt` 的内容。

 `<#@ include file="c:\test.txt" #>`

 在处理时，被包含内容就像是包含文本模板的组成部分一样。 不过，即使 include 指令后跟普通文本块和标准控制块，也可以包含编写有类功能块 `<#+...#>` 的文件。

 For more information, see [T4 Include Directive](../modeling/t4-include-directive.md).

### <a name="utility-methods"></a>实用工具方法
 在控制块中，有几个方法（如 `Write()`）始终可用。 这些方法包括可帮助缩进输出和报告错误的方法。

 你也可以编写自己的实用工具方法集。

 For more information, see [Text Template Utility Methods](../modeling/text-template-utility-methods.md).

## <a name="transforming-data-and-models"></a>转换数据和模型
 对于文本模板而言，最有用的应用是根据源（如模型、数据库或数据文件）的内容生成材料。 模板提取数据并重新设置数据格式。 模板集合可以将此类源转换为多个文件。

 有几种方法可以读取源文件。

 **Read a file in the text template**. 下面是将数据读入模板的最简单的方法：

```
<#@ import namespace="System.IO" #>
<# string fileContent = File.ReadAllText(@"C:\myData.txt"); ...
```

 **Load a file as a navigable model**. 更有效的方法是将数据作为模型读取，文本模板代码可以导航该模型。 例如，可以加载 XML 文件，然后使用 XPath 表达式对其导航。 You could also use [xsd.exe](https://go.microsoft.com/fwlink/?LinkId=178765) to create a set of classes with which you can read the XML data.

 **Edit the model file in a diagram or form.** [!INCLUDE[dsl](../includes/dsl-md.md)] provides tools that let you edit a model as a diagram or Windows form. 这样便于与生成的应用程序的用户讨论模型。 [!INCLUDE[dsl](../includes/dsl-md.md)] 还创建一组反映模型结构的强类型类。 For more information, see [Generating Code from a Domain-Specific Language](../modeling/generating-code-from-a-domain-specific-language.md).

 **Use a UML model**. 可以从 UML 模型生成代码。 这种方式的优点在于，可以以熟悉的表示法将模型作为关系图进行编辑。 此外，无需设计关系图。 For more information, see [Generate files from a UML model](../modeling/generate-files-from-a-uml-model.md).

### <a name="relative-file-paths-in-design-time-templates"></a>设计时模板中的相对文件路径
 In a [design-time text template](../modeling/design-time-code-generation-by-using-t4-text-templates.md), if you want to reference a file in a location relative to the text template, use `this.Host.ResolvePath()`. 还必须在 `hostspecific="true"` 指令中设置 `template`：

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="System.IO" #>
<#
 // Find a path within the same project as the text template:
 string myFile = File.ReadAllText(this.Host.ResolvePath("MyFile.txt"));
#>
Content of MyFile.txt is:
<#= myFile #>

```

 还可以获取主机提供的其他服务。 For more information, see [Accessing Visual Studio or other Hosts from a Template](https://msdn.microsoft.com/0556f20c-fef4-41a9-9597-53afab4ab9e4).

### <a name="design-time-text-templates-run-in-a-separate-appdomain"></a>设计时文本模板在单独的 AppDomain 中运行
 You should be aware that a [design-time text template](../modeling/design-time-code-generation-by-using-t4-text-templates.md) runs in an AppDomain that is separate from the main application. 在大多数情况下这并不重要，但在某些复杂的情况下你可能会发现一些限制。 例如，如果要从单独的服务将数据传入模板或从中传出数据，则该服务必须提供可序列化的 API。

 (This isn’t true of a [run-time text template](../modeling/run-time-text-generation-with-t4-text-templates.md), which provides code that is compiled along with the rest of your code.)

## <a name="editing-templates"></a>编辑模板
 可从扩展管理器联机库下载专用文本模板编辑器。 On the **Tools** menu, click **Extension Manager**. Click **Online Gallery**, and then use the search tool.

## <a name="related-topics"></a>相关主题

|任务|主题|
|----------|-----------|
|编写模板。|[T4 文本模板编写准则](../modeling/guidelines-for-writing-t4-text-templates.md)|
|使用程序代码生成文本。|[Text Template Structure](../modeling/writing-a-t4-text-template.md)|
|在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 解决方案中生成文件。|[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)|
|在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 外运行文本生成。|[使用 TextTransform 实用工具生成文件](../modeling/generating-files-with-the-texttransform-utility.md)|
|以域特定语言的形式转换数据。|[从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)|
|编写指令处理器转换自己的数据源。|[自定义 T4 文本转换](../modeling/customizing-t4-text-transformation.md)|
