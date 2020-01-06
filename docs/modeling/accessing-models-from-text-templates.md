---
title: 从文本模板访问模型
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, accessing models
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b9ac9fb023797db98f3b83aa4da7b92e71f0e71e
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590613"
---
# <a name="access-models-from-text-templates"></a>从文本模板访问模型

通过使用文本模板，你可以创建基于域特定语言模型的报表文件、源代码文件和其他文本文件。 有关文本模板的基本信息，请参阅[代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)。 调试 DSL 时，文本模板将在实验模式下工作，并且还可在已部署 DSL 的计算机上运行。

> [!NOTE]
> 创建 DSL 解决方案时，将在调试项目中生成示例文本模板 **\*tt**文件。 更改域类的名称时，这些模板将不再工作。 尽管如此，它们包括你需要的基本指令，并提供可进行更新以匹配 DSL 的示例。

 从文本模板访问模型：

- 将模板指令的 inherit 属性设置为[VisualStudio. TextTemplating. vshost.exe. ModelingTextTransformation](/previous-versions/bb893209(v=vs.140))。 这将提供对应用商店的访问权限。

- 为要访问的 DSL 指定指令处理器。 这会加载 DSL 的程序集，以便在文本模板的代码中使用其域类、属性和关系。 它还会加载您指定的模型文件。

  从 "DSL 最小语言" 模板创建新的 Visual Studio 解决方案时，将在调试项目中创建类似于以下示例的 `.tt` 文件。

```
<#@ template inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" #>
<#@ output extension=".txt" #>
<#@ MyLanguage processor="MyLanguageDirectiveProcessor" requires="fileName='Sample.myDsl1'" #>

This text will be output directly.

This is the name of the model: <#= this.ModelRoot.Name #>

Here is a list of elements in the model:
<#
  // When you change the DSL Definition, some of the code below may not work.
  foreach (ExampleElement element in this.ExampleModel.Elements)
  {#>
<#= element.Name #>
<#
  }
#>
```

 请注意有关此模板的以下几点：

- 模板可以使用在 DSL 定义中定义的域类、属性和关系。

- 模板加载您在 `requires` 属性中指定的模型文件。

- `this` 中的属性包含根元素。 您的代码可以在其中导航到模型的其他元素。 属性的名称通常与 DSL 的根域类相同。 在此示例中，设为 `this.ExampleModel`。

- 虽然编写代码片段的语言为C#，但你可以生成任何类型的文本。 您也可以通过将属性 `language="VB"` 添加到 `template` 指令来在 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 中编写代码。

- 若要调试模板，请将 `debug="true"` 添加到 `template` 指令中。 如果发生异常，则模板将在 Visual Studio 的另一个实例中打开。 若要在代码中的特定点中断调试器，请插入语句 `System.Diagnostics.Debugger.Break();`

   有关详细信息，请参阅[调试 T4 文本模板](../modeling/debugging-a-t4-text-template.md)。

## <a name="about-the-dsl-directive-processor"></a>关于 DSL 指令处理器
 模板可以使用在 DSL 定义中定义的域类。 这是通过通常出现在模板开头附近的指令来进行的。 在上面的示例中，它如下所示。

```
<#@ MyLanguage processor="MyLanguageDirectiveProcessor" requires="fileName='Sample.myDsl1'" #>
```

 指令的名称（在本示例中为 `MyLanguage`）派生自 DSL 的名称。 它调用作为 DSL 的一部分生成的*指令处理器*。 可以在**Dsl\GeneratedCode\DirectiveProcessor.cs**中找到它的源代码。

 DSL 指令处理器执行两个主要任务：

- 它有效地将程序集和导入指令插入到引用 DSL 的模板中。 这允许您在模板代码中使用您的域类。

- 它加载您在 `requires` 参数中指定的文件，并在 `this` 中设置引用已加载模型的根元素的属性。

## <a name="validating-the-model-before-running-the-template"></a>在运行模板之前验证模型
 您可以在执行模板之前对模型进行验证。

```
<#@ MyLanguage processor="MyLanguageDirectiveProcessor" requires="fileName='Sample.myDsl1';validation='open|load|save|menu'" #>
```

 请注意：

1. `filename` 和 `validation` 参数用 ";" 分隔，且不能有其他分隔符或空格。

2. 验证类别的列表确定将执行哪些验证方法。 应该用 "&#124;" 分隔多个类别，并且必须没有其他分隔符或空格。

   如果发现错误，将在 "错误" 窗口中报告该错误，结果文件将包含一条错误消息。

## <a name="Multiple"></a>从文本模板访问多个模型

> [!NOTE]
> 此方法使您可以读取同一模板中的多个模型，但不支持 ModelBus 引用。 若要读取由 ModelBus 引用了的模型，请参阅[在文本模板中使用 Visual Studio ModelBus](../modeling/using-visual-studio-modelbus-in-a-text-template.md)。

 如果要从同一文本模板访问多个模型，则必须为每个模型调用一次生成的指令处理器。 必须在 `requires` 参数中指定每个模型的文件名。 你必须在 `provides` 参数中指定要用于根域类的名称。 必须为每个指令调用中的 `provides` 参数指定不同的值。 例如，假定您有三个名为 Library、School 和 .xyz 的模型文件。 若要从同一文本模板访问它们，必须编写三个类似于下面的指令调用。

```
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='Library.xyz'" provides="ExampleModel=LibraryModel" #>
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='School.xyz'" provides="ExampleModel=SchoolModel" #>
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='Work.xyz'" provides="ExampleModel=WorkModel" #>
```

> [!NOTE]
> 此代码示例适用于基于最小语言解决方案模板的语言。

 若要访问文本模板中的模型，你现在可以编写类似于以下示例中的代码的代码。

```csharp
<#
foreach (ExampleElement element in this.LibraryModel.Elements)
...
foreach (ExampleElement element in this.SchoolModel.Elements)
...
foreach (ExampleElement element in this.WorkModel.Elements)
...
#>
```

```vb
<#
For Each element As ExampleElement In Me.LibraryModel.Elements
...
For Each element As ExampleElement In Me.SchoolModel.Elements
...
For Each element As ExampleElement In Me.WorkModel.Elements
...
#>
```

## <a name="loading-models-dynamically"></a>动态加载模型
 如果要在运行时确定要加载的模型，可以在程序代码中动态加载模型文件，而不是使用特定于 DSL 的指令。

 但是，DSL 专用指令的功能之一是导入 DSL 命名空间，以便模板代码可以使用该 DSL 中定义的域类。 由于您未使用指令，因此必须将 **\<程序集添加 >** 并 **\<导入**您可能加载的所有模型的 > 指令。 如果可以加载的不同模型都是同一 DSL 的所有实例，这很容易。

 若要加载该文件，最有效的方法是使用 Visual Studio ModelBus。 在典型方案中，文本模板将使用特定于 DSL 的指令以常规方式加载第一个模型。 该模型将包含对另一个模型的 ModelBus 引用。 您可以使用 ModelBus 打开引用的模型并访问特定的元素。 有关详细信息，请参阅[文本模板中使用 Visual Studio ModelBus](../modeling/using-visual-studio-modelbus-in-a-text-template.md)。

 在不太常见的情况下，你可能想要打开的模型文件只有一个文件名，并且该文件可能不在当前的 Visual Studio 项目中。 在这种情况下，可以使用[如何：在程序代码中打开文件中的模型](../modeling/how-to-open-a-model-from-file-in-program-code.md)中所述的方法来打开文件。

## <a name="generating-multiple-files-from-a-template"></a>从模板生成多个文件
 如果要生成几个文件（例如，为了为模型中的每个元素生成一个单独的文件），则有几种可能的方法。 默认情况下，每个模板文件仅生成一个文件。

### <a name="splitting-a-long-file"></a>拆分长文件
 在此方法中，您将使用一个模板生成一个文件，并用分隔符分隔。 然后，将文件拆分为其各个部分。 有两个模板，一个用于生成单个文件，另一个用于拆分。

 **LoopTemplate**生成长的单个文件。 请注意，其文件扩展名为 "t4"，因为当你单击 "**转换所有模板**" 时不应直接处理该文件扩展名。 此模板采用参数，该参数指定分隔段的分隔符字符串：

```
<#@ template ninherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" #>
<#@ parameter name="delimiter" type="System.String" #>
<#@ output extension=".txt" #>
<#@ MyDSL processor="MyDSLDirectiveProcessor" requires="fileName='SampleModel.mydsl1';validation='open|load|save|menu'" #>
<#
  // Create a file segment for each element:
  foreach (ExampleElement element in this.ExampleModel.Elements)
  {
    // First item is the delimiter:
#>
<#= string.Format(delimiter, element.Id) #>

   Element: <#= element.Name #>
<#
   // Here you generate more content derived from the element.
  }
#>
```

 `LoopSplitter.tt` 调用 `LoopTemplate.t4`，然后将生成的文件拆分为其段。 请注意，此模板不必是建模模板，因为它不会读取模型。

```
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="Microsoft.VisualStudio.TextTemplating" #>
<#@ import namespace="System.Runtime.Remoting.Messaging" #>
<#@ import namespace="System.IO" #>

<#
  // Get the local path:
  string itemTemplatePath = this.Host.ResolvePath("LoopTemplate.t4");
  string dir = Path.GetDirectoryName(itemTemplatePath);

  // Get the template for generating each file:
  string loopTemplate = File.ReadAllText(itemTemplatePath);

  Engine engine = new Engine();

  // Pass parameter to new template:
  string delimiterGuid = Guid.NewGuid().ToString();
  string delimiter = "::::" + delimiterGuid + ":::";
  CallContext.LogicalSetData("delimiter", delimiter + "{0}:::");
  string joinedFiles = engine.ProcessTemplate(loopTemplate, this.Host);

  string [] separateFiles = joinedFiles.Split(new string [] {delimiter}, StringSplitOptions.None);

  foreach (string nameAndFile in separateFiles)
  {
     if (string.IsNullOrWhiteSpace(nameAndFile)) continue;
     string[] parts = nameAndFile.Split(new string[]{":::"}, 2, StringSplitOptions.None);
     if (parts.Length < 2) continue;
#>
 Generate: [<#= dir #>] [<#= parts[0] #>]
<#
     // Generate a file from this item:
     File.WriteAllText(Path.Combine(dir, parts[0] + ".txt"), parts[1]);
  }
#>
```
