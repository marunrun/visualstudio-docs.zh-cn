---
title: 演练：调试访问模型的文本模板
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f592cfbd46e0f4fc3a64ecaabadf17a6754480c0
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593520"
---
# <a name="walkthrough-debugging-a-text-template-that-accesses-a-model"></a>演练：调试访问模型的文本模板
在域特定语言解决方案中修改或添加文本模板时，当引擎将模板转换为源代码或编译生成的代码时，可能会出现错误。 以下演练演示了调试文本模板时可以执行的一些操作。

> [!NOTE]
> 有关一般文本模板的详细信息，请参阅[代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)。 有关调试文本模板的详细信息，请参阅[演练：调试文本模板](debugging-a-t4-text-template.md)。

## <a name="creating-a-domain-specific-language-solution"></a>创建域特定语言解决方案
 在此过程中，您将创建一个具有以下特征的域特定语言解决方案：

- 名称： DebuggingTestLanguage

- 解决方案模板：最小语言

- 文件扩展名： ddd

- 公司名称： Fabrikam

  有关创建域特定语言解决方案的详细信息，请参阅[如何：创建特定于域的语言解决方案](../modeling/how-to-create-a-domain-specific-language-solution.md)。

## <a name="creating-a-text-template"></a>创建文本模板
 向解决方案添加文本模板。

#### <a name="to-create-a-text-template"></a>创建文本模板

1. 生成解决方案并开始在调试器中运行。 （在 "**生成**" 菜单上，单击 "**重新生成解决方案**"，然后在 "**调试**" 菜单上单击 "**启动调试**"。）Visual Studio 的新实例将打开调试项目。

2. 向调试项目添加一个名为 `DebugTest.tt` 的文本文件。

3. 确保将 DebugTest.tt 的 "**自定义工具**" 属性设置为 `TextTemplatingFileGenerator`。

## <a name="debugging-directives-that-access-a-model-from-a-text-template"></a>从文本模板访问模型的调试指令
 必须先调用生成的指令处理器，然后才能从文本模板中的语句和表达式访问模型。 调用生成的指令处理器会使模型中的类可用于文本模板代码作为属性。 有关详细信息，请参阅[从文本模板访问模型](../modeling/accessing-models-from-text-templates.md)。

 在下面的过程中，您将调试错误的指令名称和不正确的属性名称。

#### <a name="to-debug-an-incorrect-directive-name"></a>调试错误的指令名称

1. 将 DebugTest.tt 中的代码替换为以下代码：

    > [!NOTE]
    > 代码包含错误。 你正在引入错误，以便对其进行调试。

    ```csharp
    <#@ template language="C#" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ modelRoot processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>

    Model: <#= this.ExampleModel #>
    <#
    foreach (ExampleElement element in this.ExampleModel.Elements)
    {
    #>
        Element: <#= element.Name #>
    <#
    }
    #>
    ```

    ```vb
    <#@ template language="VB" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ modelRoot processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>

    Model: <#= Me.ExampleModel #>
    <#
    For Each element as ExampleElement in Me.ExampleModel.Elements
    #>
        Element: <#= element.Name #>
    <#
    Next
    #>
    ```

2. 在**解决方案资源管理器**中，右键单击 DebugTest.tt，然后单击 "**运行自定义工具**"。

     "**错误列表**" 窗口显示此错误：

     **名为 "DebuggingTestLanguageDirectiveProcessor" 的处理器不支持名为 "modelRoot" 的指令。转换将不会运行。**

     在这种情况下，指令调用包含错误的指令名称。 您已将 `modelRoot` 指定为指令名称，但 `DebuggingTestLanguage`了正确的指令名称。

3. 双击 "**错误列表**" 窗口中的错误，跳转到代码。

4. 若要更正此代码，请将指令名称更改为 `DebuggingTestLanguage`。

     更改将突出显示。

    ```csharp
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>
    ```

    ```vb
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>
    ```

5. 在**解决方案资源管理器**中，右键单击 DebugTest.tt，然后单击 "**运行自定义工具**"。

     系统现在会转换文本模板并生成相应的输出文件。 "**错误列表**" 窗口中将不会显示任何错误。

#### <a name="to-debug-an-incorrect-property-name"></a>调试错误的属性名称

1. 将 DebugTest.tt 中的代码替换为以下代码：

    > [!NOTE]
    > 代码包含错误。 你正在引入错误，以便对其进行调试。

    ```csharp
    <#@ template language="C#" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>

    Model: <#= this.ExampleModel #>
    <#
    foreach (ExampleElement element in this.ExampleModel.Elements)
    {
    #>
        Element: <#= element.Name #>
    <#
    }
    #>
    ```

    ```vb
    <#@ template language="VB" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>

    Model: <#= Me.ExampleModel #>
    <#
    For Each element as ExampleElement in Me.ExampleModel.Elements
    #>
        Element: <#= element.Name #>
    <#
    Next
    #>
    ```

2. 在**解决方案资源管理器**中，右键单击 DebugTest.tt，然后单击 "**运行自定义工具**"。

     此时将显示 "**错误列表**" 窗口，并显示以下错误之一：

     (C#)

     **编译转换： VisualStudio. TextTemplating\<GUID >。GeneratedTextTransformation "不包含" 位于 examplemodel.store "的定义**

     （Visual Basic）

     **编译转换： "位于 examplemodel.store" 不是 "TextTemplating\<GUID > 的成员。GeneratedTextTransformation'.**

     在这种情况下，文本模板代码包含不正确的属性名称。 已将 `ExampleModel` 指定为属性名称，但 `LibraryModel`正确的属性名称。 可以在提供参数中找到正确的属性名称，如下面的代码所示：

    ```
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>
    ```

3. 双击 "错误列表" 窗口中的错误，跳转到代码。

4. 若要更正此代码，请在文本模板代码中将属性名称更改为 `LibraryModel`。

     突出显示所作更改。

    ```csharp
    <#@ template language="C#" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>

    Model: <#= this.LibraryModel #>
    <#
    foreach (ExampleElement element in this.LibraryModel.Elements)
    {
    #>
        Element: <#= element.Name #>
    <#
    }
    #>
    ```

    ```vb
    <#@ template language="VB" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation"#>
    <#@ output extension=".txt" #>
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>

    Model: <#= Me.LibraryModel #>
    <#
    For Each element as ExampleElement in Me.LibraryModel.Elements
    #>
        Element: <#= element.Name #>
    <#
    Next
    #>
    ```

5. 在**解决方案资源管理器**中，右键单击 DebugTest.tt，然后单击 "**运行自定义工具**"。

     系统现在会转换文本模板并生成相应的输出文件。 "**错误列表**" 窗口中将不会显示任何错误。
