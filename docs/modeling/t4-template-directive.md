---
title: T4 模板指令
ms.date: 11/04/2016
ms.topic: reference
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 410bc879ff4822f19436794d3cb99732be9d413e
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72983708"
---
# <a name="t4-template-directive"></a>T4 模板指令

Visual Studio T4 文本模板通常以 `template` 指令开头，该指令指定如何处理模板。 文本模板及其包括的任何文件中不应有多个 template 指令。

有关编写文本模板的一般概述，请参阅[编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)。

## <a name="using-the-template-directive"></a>使用 Template 指令

```
<#@ template [language="VB"] [compilerOptions="options"] [culture="code"] [debug="true"] [hostspecific="true"] [inherits="templateBaseClass"] [visibility="internal"] [linePragmas="false"] #>
```

`template` 指令有多个特性，通过这些特性可以指定转换的不同方面。 所有特性都是可选的。

## <a name="compileroptions-attribute"></a>compilerOptions 特性

示例:

`compilerOptions="optimize+"`

有效值：

任何有效的编译器选项。

对运行时（预处理过的）模板忽略。

在模板已经转换为 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 或 [!INCLUDE[vb_current_short](../debugger/includes/vb_current_short_md.md)] 并且生成的代码已编译时会应用这些选项。

## <a name="culture-attribute"></a>culture 特性

示例:

`culture="de-CH"`

有效值：

""，不变的区域性，它是默认值。

表示为 xx-XX 形式字符串的区域性。 例如：en-US、ja-JP、de-CH、de-DE。 有关更多信息，请参见<xref:System.Globalization.CultureInfo?displayProperty=fullName>。

Culture 特性指定将表达式块转换为文本时要使用的区域性。

## <a name="debug-attribute"></a>debug 特性

示例:

```
debug="true"
```

有效值：

`true`

`false`（默认值）

如果 `debug` 特性为 `true`，则中间代码文件将包含使调试器能够更精确地识别模板中出现中断或异常的位置的信息。

对于设计时模板，中间代码文件将写入你的 **% TEMP%** 目录。

若要在调试器中运行设计时模板，请保存文本模板，然后在解决方案资源管理器中打开文本模板的快捷菜单，然后选择 "**调试 T4 模板**"。

## <a name="hostspecific-attribute"></a>hostspecific 特性

示例:

```
hostspecific="true"
```

有效值：

`true`

`false`（默认值）

`trueFromBase`

如果将此特性的值设置为 `true`，则会将名为 `Host` 的属性添加到由文本模板生成的类中。 该属性是对转换引擎的主机的引用，并声明为[ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))。 如果已经定义了自定义宿主，则可以将其转换为自定义宿主类型。

因为此属性的类型取决于宿主的类型，所以仅当编写只适用于特定宿主的文本模板时才有用。 它适用于[设计时模板](../modeling/design-time-code-generation-by-using-t4-text-templates.md)，但不适用于[运行时模板](../modeling/run-time-text-generation-with-t4-text-templates.md)。

当 `true` `hostspecific` 并且使用的是 Visual Studio 时，可以将 `this.Host` 强制转换为 IServiceProvider，以便访问 Visual Studio 功能。 还可以使用 `Host.ResolvePath(filename)` 来获得项目中文件的绝对路径。 例如:

```csharp
<#@ template debug="false" hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ assembly name="EnvDTE" #>
<#@ import namespace="EnvDTE" #>
<#@ import namespace="System.IO" #>
<#@ import namespace="Microsoft.VisualStudio.TextTemplating" #>
<# // Get the Visual Studio API as a service:
 DTE dte = ((IServiceProvider)this.Host).GetCOMService(typeof(DTE)) as DTE;
#>
Number of projects in this solution: <#=  dte.Solution.Projects.Count #>

<#
 // Find a path within the current project:
 string myFile = File.ReadAllText(this.Host.ResolvePath("MyFile.txt"));
#>
Content of myFile is:
<#= myFile #>
```

如果同时使用 `inherits` 和 `hostspecific` 特性，则请在派生类和基类中分别指定 host="trueFromBase" 和 host="true"。 这样可避免双重定义生成代码中的 `Host` 属性。

## <a name="language-attribute"></a>language 特性

示例:

`language="VB"`

有效值：

`C#`（默认值）

`VB`

`language` 特性指定用于语句和表达式块中的源代码的语言（[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 或 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]）。 从中生成输出的中间代码文件将使用此语言。 此语言与您的模板生成的语言无关，它可以是任何类型的文本。

例如:

```vb
<#@ template language="VB" #>
<#@ output extension=".txt" #>
Squares of numbers:
<#
  Dim number As Integer
  For number = 1 To 4
#>
  Square of <#= number #> is <#= number * number #>
<#
  Next number
#>
```

## <a name="inherits-attribute"></a>inherits 特性

可以指定模板的程序代码可以继承自另一个类，这个类也可以从文本模板生成。

### <a name="inheritance-in-a-run-time-preprocessed-text-template"></a>运行时（预处理过的）文本模板中的继承

可以在运行时文本模板之间使用继承，来创建具有多个派生变量的基本模板。 运行时模板是将 "**自定义工具**" 属性设置为 " **TextTemplatingFilePreprocessor**" 的模板。 运行时模板生成你可以在应用程序中调用的代码，以便创建模板中定义的文本。 有关详细信息，请参阅[带有 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)。

如果不指定 `inherits` 特性，则会从您的文本模板生成基类和派生类。 指定 `inherits` 特性时，仅生成派生类。 您可以手动编写基类，但是它必须提供派生类所使用的方法。

更通常的做法是，指定另一个预处理过的模板作为基类。 基模板提供通用文本块，它们可与来自派生模板的文本交错在一起。 可以使用类功能块 `<#+ ... #>` 来定义包含文本段落的方法。 例如，可以在基模板中放置输出文本的框架，从而提供可在派生模板中重写的虚拟方法。

运行时（预处理过的）文本模板 BaseTemplate.tt：

```scr
This is the common header.
<#
  SpecificFragment1();
#>
A common central text.
<#
  SpecificFragment2();
#>
This is the common footer.
<#+
  // Declare abstract methods
  protected virtual void SpecificFragment1() { }
  protected virtual void SpecificFragment2() { }
#>
```

运行时（预处理过的）文本模板 DerivedTemplate1.tt：

```csharp
<#@ template language="C#" inherits="BaseTemplate" #>
<#
  // Run the base template:
  base.TransformText();
#>
<#+
// Provide fragments specific to this derived template:
protected override void SpecificFragment1()
{
#>
   Fragment 1 for DerivedTemplate1
<#+
}
protected override void SpecificFragment2()
{
#>
   Fragment 2 for DerivedTemplate1
<#+
}
#>
```

用于调用 DerivedTemplate1 的应用程序代码：

```csharp
Console.WriteLine(new DerivedTemplate().TransformText());
```

结果输出：

```
This is the common header.
   Fragment 1 for DerivedTemplate1
A common central text.
   Fragment 2 for DerivedTemplate1
This is the common footer.
```

可以在不同的项目中构建基类和派生类。 请记得向派生项目的引用添加基本项目或程序集。

还可以使用普通手写类作为基类。 基类必须提供派生类使用的方法。

> [!WARNING]
> 如果同时使用 `inherits` 和 `hostspecific` 特性，则请在派生类和基类中分别指定 hostspecific="trueFromBase" 和 host="true"。 这样可避免双重定义生成代码中的 `Host` 属性。

### <a name="inheritance-in-a-design-time-text-template"></a>设计时文本模板中的继承

设计时文本模板是**自定义工具**设置为**TextTemplatingFileGenerator**的文件。 该模板将生成代码或文本的输出文件，该文件构成了你的 Visual Studio 项目的一部分。 若要生成输出文件，首先要将模板转换为中间程序代码文件，你通常不会看到该文件。 `inherits` 特性为此中间代码指定基类。

对于设计时文本模板来说，可以指定从 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation?displayProperty=fullName> 派生的任何基类。 使用 `<#@assembly#>` 指令来加载包含基类的程序集或项目。

有关详细信息，请参阅[Gareth 的 "博客中的" 文本模板中的继承 "](https://blogs.msdn.microsoft.com/garethj/2011/01/03/vs2010-sp1-t4-template-inheritance-part-i-sample-metadata/)。

## <a name="linepragmas-attribute"></a>linePragmas 特性

示例:

`linePragmas="false"`

有效值：

`true`（默认值）

`false`

将此特性设置为 false 将移除标识你在生成代码中的行号的标记。 这意味着，编译器将通过使用生成代码的行号来报告所有错误。这将为你提供更多调试选项，如你可选择调试文本模板或生成代码。

如果要在杂注中查找绝对文件名，会导致源代码管理下的合并产生混乱，此属性也会有所帮助。

## <a name="visibility-attribute"></a>visibility 特性

示例:

`visibility="internal"`

有效值：

`public`（默认值）

`internal`

在运行时文本模板中，这将设置生成类的可见性特性。 默认情况下，此类是你代码的公共 API 的一部分，但通过设置 `visibility="internal"`，你可以确保仅你的代码可使用文本生成类。
