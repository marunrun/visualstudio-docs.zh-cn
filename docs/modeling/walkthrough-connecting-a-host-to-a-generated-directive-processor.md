---
title: 将主机连接到生成的指令处理器
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- walkthroughs [text templates], connecting host to processor
- text templates, custom directive hosts
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
dev_langs:
- CSharp
- VB
ms.openlocfilehash: a27b856b9c5129f725381afa34bd134009002216
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593975"
---
# <a name="walkthrough-connect-a-host-to-a-generated-directive-processor"></a>演练：将主机连接到生成的指令处理器

您可以编写自己的宿主来处理文本模板。 [演练：创建自定义文本模板宿主](../modeling/walkthrough-creating-a-custom-text-template-host.md)中演示了一个基本的自定义主机。 您可以扩展该主机以添加功能，如生成多个输出文件。

在本演练中，将展开自定义主机，使其支持调用指令处理器的文本模板。 定义域特定语言时，它将为域模型生成*指令处理器*。 指令处理器使用户能够更轻松地编写访问该模型的模板，从而减少了在模板中编写程序集和导入指令的需求。

> [!NOTE]
> 本演练基于[演练：创建自定义文本模板宿主](../modeling/walkthrough-creating-a-custom-text-template-host.md)。 首先执行该演练。

本演练包含以下任务：

- 使用 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 生成基于域模型的指令处理器。

- 将自定义文本模板宿主连接到生成的指令处理器。

- 用生成的指令处理器测试自定义主机。

## <a name="prerequisites"></a>先决条件

若要定义 DSL，必须安装以下组件：

| | |
|-|-|
| Visual Studio | [http://go.microsoft.com/fwlink/?LinkId=185579](https://visualstudio.microsoft.com/) |
| [!INCLUDE[vssdk_current_short](../modeling/includes/vssdk_current_short_md.md)] | [http://go.microsoft.com/fwlink/?LinkId=185580](/azure/devops/integrate/index) |
| Visual Studio 可视化和建模 SDK | |

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

此外，还必须在[演练：创建自定义文本模板宿主](../modeling/walkthrough-creating-a-custom-text-template-host.md)中创建自定义文本模板转换。

## <a name="use-domain-specific-language-tools-to-generate-a-directive-processor"></a>使用特定于域的语言工具生成指令处理器

在本演练中，将使用特定于域的语言设计器向导为解决方案 DSLMinimalTest 创建域特定语言。

1. 创建具有以下特征的域特定语言解决方案：

   - 名称： DSLMinimalTest

   - 解决方案模板：最小语言

   - 文件扩展名：最小值

   - 公司名称： Fabrikam

   有关创建域特定语言解决方案的详细信息，请参阅[如何：创建特定于域的语言解决方案](../modeling/how-to-create-a-domain-specific-language-solution.md)。

2. 在 **“生成”** 菜单上，单击 **“生成解决方案”** 。

   > [!IMPORTANT]
   > 此步骤将生成指令处理器，并在注册表中为其添加密钥。

3. 在“调试”菜单上，单击“启动调试”。

    此时将打开 Visual Studio 的第二个实例。

4. 在实验生成的**解决方案资源管理器**中，双击文件**示例。**

    文件将在设计器中打开。 请注意，该模型包含两个元素（ExampleElement1 和 ExampleElement2）以及它们之间的链接。

5. 关闭 Visual Studio 的第二个实例。

6. 保存解决方案，然后关闭特定于域的语言设计器。

## <a name="connect-a-custom-text-template-host-to-a-directive-processor"></a>将自定义文本模板主机连接到指令处理器

生成指令处理器后，将连接在[演练：创建自定义文本模板主机](../modeling/walkthrough-creating-a-custom-text-template-host.md)中创建的指令处理器和自定义文本模板主机。

1. 打开 CustomHost 解决方案。

2. 在“项目”菜单上，单击“添加引用”。

     此时将打开 "**添加引用**" 对话框，其中显示了 " **.net** " 选项卡。

3. 添加以下引用：

    - Microsoft.VisualStudio.Modeling.Sdk.11.0

    - Microsoft.VisualStudio.Modeling.Sdk.Diagrams.11.0

    - Microsoft.VisualStudio.TextTemplating.11.0

    - Microsoft.VisualStudio.TextTemplating.Interfaces.11.0

    - Microsoft.VisualStudio.TextTemplating.Modeling.11.0

    - Microsoft.VisualStudio.TextTemplating.VSHost.11.0

4. 在 Program.cs 或 Module1 的顶部，添加以下代码行：

    ```csharp
    using Microsoft.Win32;
    ```

    ```vb
    Imports Microsoft.Win32
    ```

5. 找到 `StandardAssemblyReferences`属性的代码，并将其替换为以下代码：

    > [!NOTE]
    > 在此步骤中，你将添加对你的主机将支持的生成的指令处理器所需的程序集的引用。

    ```csharp
    //the host can provide standard assembly references
    //the engine will use these references when compiling and
    //executing the generated transformation class
    //--------------------------------------------------------------
    public IList<string> StandardAssemblyReferences
    {
        get
        {
            return new string[]
            {
                //if this host searches standard paths and the GAC
                //we can specify the assembly name like this:
                //"System"
                //since this host only resolves assemblies from the
                //fully qualified path and name of the assembly
                //this is a quick way to get the code to give us the
                //fully qualified path and name of the System assembly
                //---------------------------------------------------------
                typeof(System.Uri).Assembly.Location,
                            typeof(System.Uri).Assembly.Location,
                typeof(Microsoft.VisualStudio.Modeling.ModelElement).Assembly.Location,
                typeof(Microsoft.VisualStudio.Modeling.Diagrams.BinaryLinkShape).Assembly.Location,
                typeof(Microsoft.VisualStudio.TextTemplating.VSHost.ITextTemplating).Assembly.Location,
                typeof(Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation).Assembly.Location

            };
        }
    }
    ```

6. 找到函数 `ResolveDirectiveProcessor`的代码，并将其替换为以下代码：

    > [!IMPORTANT]
    > 此代码包含对要连接到的所生成指令处理器名称的硬编码引用。 您可以轻松地使此方法更常规，在这种情况下，它会查找注册表中列出的所有指令处理器，并尝试找到匹配项。 在这种情况下，主机将适用于任何生成的指令处理器。

    ```csharp
    //the engine calls this method based on the directives the user has
            //specified it in the text template
            //this method can be called 0, 1, or more times
            //---------------------------------------------------------------------
            public Type ResolveDirectiveProcessor(string processorName)
            {
                //check the processor name, and if it is the name of the processor the
                //host wants to support, return the type of the processor
                //---------------------------------------------------------------------
                if (string.Compare(processorName, "DSLMinimalTestDirectiveProcessor", StringComparison.InvariantCultureIgnoreCase) == 0)
                {
                    try
                    {
                        string keyName = @"Software\Microsoft\VisualStudio\10.0Exp_Config\TextTemplating\DirectiveProcessors\DSLMinimalTestDirectiveProcessor";
                        using (RegistryKey specificKey = Registry.CurrentUser.OpenSubKey(keyName))
                        {
                            if (specificKey != null)
                            {
                                List<string> names = new List<String>(specificKey.GetValueNames());
                                string classValue = specificKey.GetValue("Class") as string;
                                if (!string.IsNullOrEmpty(classValue))
                                {
                                    string loadValue = string.Empty;
                                    System.Reflection.Assembly processorAssembly = null;
                                    if (names.Contains("Assembly"))
                                    {
                                        loadValue = specificKey.GetValue("Assembly") as string;
                                        if (!string.IsNullOrEmpty(loadValue))
                                        {
                                            //the assembly must be installed in the GAC
                                            processorAssembly = System.Reflection.Assembly.Load(loadValue);
                                        }
                                    }
                                    else if (names.Contains("CodeBase"))
                                    {
                                        loadValue = specificKey.GetValue("CodeBase") as string;
                                        if (!string.IsNullOrEmpty(loadValue))
                                        {
                                            //loading local assembly
                                            processorAssembly = System.Reflection.Assembly.LoadFrom(loadValue);
                                        }
                                    }
                                    if (processorAssembly == null)
                                    {
                                        throw new Exception("Directive Processor not found");
                                    }
                                    Type processorType = processorAssembly.GetType(classValue);
                                    if (processorType == null)
                                    {
                                        throw new Exception("Directive Processor not found");
                                    }
                                    return processorType;
                                }
                            }
                        }
                    }
                    catch (Exception e)
                    {
                        //if the directive processor can not be found, throw an error
                        throw new Exception("Directive Processor not found");
                    }
                }

                //if the directive processor is not one this host wants to support
                throw new Exception("Directive Processor not supported");
            }
    ```

7. 在“文件”菜单上，单击“全部保存”。

8. 在 **“生成”** 菜单上，单击 **“生成解决方案”** 。

## <a name="test-the-custom-host-with-the-directive-processor"></a>用指令处理器测试自定义主机

若要测试自定义文本模板宿主，首先必须编写一个调用生成的指令处理器的文本模板。 然后，运行自定义主机，向其传递文本模板的名称，并验证是否已正确处理指令。

### <a name="create-a-text-template-to-test-the-custom-host"></a>创建文本模板以测试自定义主机

1. 创建一个文本文件，并将其命名为 `TestTemplateWithDP.tt`。 您可以使用任何文本编辑器（例如记事本）来创建该文件。

2. 向文本文件中添加以下内容：

    > [!NOTE]
    > 文本模板的编程语言不需要与自定义宿主的编程语言匹配。

    ```csharp
    Text Template Host Test

    <#@ template debug="true" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" #>
    <# //this is the call to the examplemodel directive in the generated directive processor #>
    <#@ DSLMinimalTest processor="DSLMinimalTestDirectiveProcessor" requires="fileName='<Your Path>\Sample.min'" provides="ExampleModel=ExampleModel" #>
    <# //uncomment this line to test that the host allows the engine to set the extension #>
    <# //@ output extension=".htm" #>

    <# //uncomment this line if you want to see the generated transformation class #>
    <# //System.Diagnostics.Debugger.Break(); #>
    <# //this code uses the results of the examplemodel directive #>
    <#
        foreach ( ExampleElement box in this.ExampleModel.Elements )
        {
            WriteLine("Box: {0}", box.Name);

            foreach (ExampleElement linkedTo in box.Targets)
            {
                WriteLine("Linked to: {0}", linkedTo.Name);
            }

            foreach (ExampleElement linkedFrom in box.Sources)
            {
                WriteLine("Linked from: {0}", linkedFrom.Name);
            }

            WriteLine("");
        }
    #>
    ```

    ```vb
    Text Template Host Test

    <#@ template debug="true" language="VB" inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" #>

    <# 'this is the call to the examplemodel directive in the generated directive processor #>
    <#@ DSLMinimalTest processor="DSLMinimalTestDirectiveProcessor" requires="fileName='<Your Path>\Sample.min'" provides="ExampleModel=ExampleModel" #>

    <# 'Uncomment this line to test that the host allows the engine to set the extension. #>
    <# '@ output extension=".htm" #>

    <# 'Uncomment this line if you want to see the generated transformation class. #>
    <# 'System.Diagnostics.Debugger.Break() #>

    <# 'this code uses the results of the examplemodel directive #>

    <#
       For Each box as ExampleElement In Me.ExampleModel.Elements

           WriteLine("Box: {0}", box.Name)

            For Each LinkedTo as ExampleElement In box.Targets
                WriteLine("Linked to: {0}", LinkedTo.Name)
            Next

            For Each LinkedFrom as ExampleElement In box.Sources
                WriteLine("Linked from: {0}", LinkedFrom.Name)
            Next

            WriteLine("")

       Next
    #>
    ```

3. 在代码中，将路径 \<替换为在第一个过程中创建的特定于设计语言的示例文件的路径 >。

4. 保存并关闭文件。

### <a name="test-the-custom-host"></a>测试自定义主机

1. 打开命令提示符窗口。

2. 为自定义宿主键入可执行文件的路径，但暂不要按 Enter。

     例如，键入：

     `<YOUR PATH>CustomHost\bin\Debug\CustomHost.exe`

    > [!NOTE]
    > 您可以在**Windows 资源管理器**中浏览到文件 CustomHost，然后将该文件拖入命令提示符窗口，而不是键入地址。

3. 键入一个空格。

4. 键入文本模板文件的路径，然后按 Enter。

     例如，键入：

     `<YOUR PATH>TestTemplateWithDP.txt`

    > [!NOTE]
    > 您可以在**Windows 资源管理器**中浏览到文件 TestTemplateWithDP，然后将该文件拖入命令提示符窗口，而不是键入地址。

     自定义主机应用程序将运行并启动文本模板转换过程。

5. 在**Windows 资源管理器**中，浏览到包含文件 TestTemplateWithDP 的文件夹。

     该文件夹还包含文件 TestTemplateWithDP1。

6. 打开此文件可以查看文本模板转换的结果。

     此时将显示生成的文本输出的结果，如下所示：

    ```
    Text Template Host Test

    Box: ExampleElement1
    Linked to: ExampleElement2

    Box: ExampleElement2
    Linked from: ExampleElement1
    ```

## <a name="see-also"></a>另请参阅

- [演练：创建自定义文本模板宿主](../modeling/walkthrough-creating-a-custom-text-template-host.md)
