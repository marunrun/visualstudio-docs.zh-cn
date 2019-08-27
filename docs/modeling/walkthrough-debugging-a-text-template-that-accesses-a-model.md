---
title: 演练：调试文本模板访问模型
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7e8b1ff717931286c5aa3aaaa69510ce05fb39a6
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385973"
---
# <a name="walkthrough-debugging-a-text-template-that-accesses-a-model"></a>演练：调试文本模板访问模型
当您修改或在域特定语言解决方案中添加文本模板时，可能会收到错误，当引擎转换模板源代码或对其进行编译生成的代码。 下面的演练演示了一些可以执行的操作来调试文本模板。

> [!NOTE]
> 详细了解文本模板一般情况下，请参阅[代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)。 有关调试文本模板的详细信息，请参阅[演练：调试文本模板](debugging-a-t4-text-template.md)。

## <a name="creating-a-domain-specific-language-solution"></a>创建域特定语言解决方案
 在此过程中，你创建域特定语言解决方案具有以下特征：

- 姓名:DebuggingTestLanguage

- 解决方案模板：最小语言

- 文件扩展名：.ddd

- 公司名称：Fabrikam

  有关创建域特定语言解决方案的详细信息，请参阅[如何：创建域特定语言解决方案](../modeling/how-to-create-a-domain-specific-language-solution.md)。

## <a name="creating-a-text-template"></a>创建文本模板
 将文本模板添加到你的解决方案。

#### <a name="to-create-a-text-template"></a>若要创建文本模板

1. 生成解决方案并启动调试器中运行。 (在**构建**菜单上，单击**重新生成解决方案**，然后在**调试**菜单上，单击**开始调试**。)Visual Studio 的新实例打开调试项目。

2. 添加一个名为文本文件`DebugTest.tt`到调试项目。

3. 请确保**自定义工具**DebugTest.tt 属性设置为`TextTemplatingFileGenerator`。

## <a name="debugging-directives-that-access-a-model-from-a-text-template"></a>从文本模板访问模型的调试指令
 您可以从语句和表达式中的文本模板访问模型之前，必须首先调用生成的指令处理器。 调用生成的指令处理器将使类在模型中供文本模板代码作为属性。 有关详细信息，请参阅[从文本模板访问模型](../modeling/accessing-models-from-text-templates.md)。

 在以下过程中，将调试不正确的指令名称和不正确的属性名称。

#### <a name="to-debug-an-incorrect-directive-name"></a>若要调试不正确的指令名称

1. DebugTest.tt 中的代码替换为以下代码：

    > [!NOTE]
    > 该代码包含一个错误。 若要调试它引入了错误。

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

2. 在中**解决方案资源管理器**，右键单击 DebugTest.tt，，然后单击**运行自定义工具**。

     **错误列表**窗口会显示此错误：

     **名为 DebuggingTestLanguageDirectiveProcessor 处理器不支持名为根本的指令。该转换将不会运行。**

     在这种情况下，指令调用包含不正确的指令名称。 具有指定`modelRoot`原样指令的名称，但正确指令名称`DebuggingTestLanguage`。

3. 双击中的错误**错误列表**窗口跳转到代码。

4. 若要更正此代码，更改到的指令名称`DebuggingTestLanguage`。

     此更改会突出显示。

    ```csharp
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>
    ```

    ```vb
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=ExampleModel" #>
    ```

5. 在中**解决方案资源管理器**，右键单击 DebugTest.tt，，然后单击**运行自定义工具**。

     现在系统转换文本模板，并生成相应的输出文件。 你将看不到中的任何错误**错误列表**窗口。

#### <a name="to-debug-an-incorrect-property-name"></a>若要调试的错误的属性名称

1. DebugTest.tt 中的代码替换为以下代码：

    > [!NOTE]
    > 该代码包含一个错误。 若要调试它引入了错误。

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

2. 在中**解决方案资源管理器**，右键单击 DebugTest.tt，，然后单击**运行自定义工具**。

     **错误列表**窗口随即出现并显示以下错误之一：

     (C#)

     **正在编译转换：Microsoft.VisualStudio.TextTemplating\<GUID>.GeneratedTextTransformation 不包含 ExampleModel 的定义**

     (Visual Basic)

     **正在编译转换：ExampleModel 不是成员的由 Microsoft.VisualStudio.TextTemplating\<GUID >。GeneratedTextTransformation。**

     在这种情况下，文本模板代码包含不正确的属性名称。 具有指定`ExampleModel`作为属性名称，但正确的属性名称是`LibraryModel`。 您可以找到正确的属性名称中提供参数，如下面的代码中所示：

    ```
    <#@ DebuggingTestLanguage processor="DebuggingTestLanguageDirectiveProcessor" requires="fileName='Sample.ddd'" provides="ExampleModel=LibraryModel" #>
    ```

3. 双击错误列表窗口来跳转到代码中的错误。

4. 若要更正代码，将属性名称更改为`LibraryModel`文本模板代码中。

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

5. 在中**解决方案资源管理器**，右键单击 DebugTest.tt，，然后单击**运行自定义工具**。

     现在系统转换文本模板，并生成相应的输出文件。 你将看不到中的任何错误**错误列表**窗口。