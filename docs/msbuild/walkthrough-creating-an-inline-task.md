---
title: 演练：创建内联任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, tutorial
- MSBuild, tasks
ms.assetid: 438194cb-668c-41a9-a7e2-c118d14c1ea7
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1d5c40af3e60add88948f8f1c5c36abf3b980eca
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2020
ms.locfileid: "77271170"
---
# <a name="walkthrough-create-an-inline-task"></a>演练：创建内联任务
通常，MSBuild 任务通过编译实现 <xref:Microsoft.Build.Framework.ITask> 接口的类进行创建。 从 .NET Framework 版本 4 开始，可以在项目文件中创建内联任务。 无需创建单独的程序集来承载该任务。 有关详细信息，请参阅[内联任务](../msbuild/msbuild-inline-tasks.md)。

 此演练演示如何创建和运行以下内联任务：

- 不具有任何输入参数或输出参数的任务。

- 具有一个输入参数但不具有输出参数的任务。

- 具有两个输入参数且具有一个返回 MSBuild 属性的输出参数的任务。

- 具有两个输入参数且具有一个返回 MSBuild 项的输出参数的任务。

若要创建并运行这些任务，请使用 Visual Studio 和 **Visual Studio 命令提示符窗口**，如下所示：

1. 使用 Visual Studio 创建一个 MSBuild 项目文件。

2. 在 Visual Studio 中修改此项目文件来创建内联任务。

3. 使用**命令提示符窗口**生成项目并检查结果。

## <a name="create-and-modify-an-msbuild-project"></a>创建和修改 MSBuild 项目
 Visual Studio 项目系统以 MSBuild 为基础。 因此，可使用 Visual Studio 创建生成项目文件。 本部分将创建 Visual C# 项目文件。 （也可创建 Visual Basic 项目文件。 在本教程的上下文中，两种项目文件间的差异很小。）

#### <a name="to-create-and-modify-a-project-file"></a>创建和修改项目文件

1. 在 Visual Studio 中的“文件”  菜单上，单击“新建”  ，然后单击“项目”  。

2. 在“新建项目”  对话框中，选择“Visual C#”  项目类型，然后选择“Windows 窗体应用程序”  模板。 在“名称”  框中键入 `InlineTasks`。 键入解决方案的“位置”  ，例如 D:\\。  请确保选择“创建解决方案目录”  和清除“添加到源代码管理”  ，并确保“解决方案名称”  为 InlineTasks。 

3. 单击“确定”  创建项目文件。

3. 在“解决方案资源管理器”  中，右键单击 InlineTasks 项目节点，然后单击“卸载项目”  。 

4. 再次右键单击项目节点，然后单击“编辑 InlineTasks.csproj”  。

     该项目文件出现在代码编辑器中。

## <a name="add-a-basic-hello-task"></a>添加基本 Hello 任务
 现在，向项目文件添加一个显示消息“Hello, world!”的基本任务。 同时添加一个用以调用此任务的默认 TestBuild 目标。

#### <a name="to-add-a-basic-hello-task"></a>添加基本 Hello 任务

1. 在根 `Project` 节点中，将 `DefaultTargets` 属性更改为 `TestBuild`。生成的 `Project` 节点应类似于本示例：

   ```xml
   <Project ToolsVersion="4.0" DefaultTargets="TestBuild" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
   ```

2. 在 `</Project>` 标记之前将如下内联任务和目标添加到项目文件。

   ```xml
   <UsingTask TaskName="Hello" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v4.0.dll" >
     <ParameterGroup />
     <Task>
       <Code Type="Fragment" Language="cs">
         Log.LogMessage(MessageImportance.High, "Hello, world!");
       </Code>
     </Task>
   </UsingTask>
   <Target Name="TestBuild">
     <Hello />
   </Target>
   ```

3. 保存项目文件。

   此代码会创建一个名为 Hello 的内联任务，且不具有任何参数、引用或 `Using` 指令。 此 Hello 任务仅包含一行代码，这行代码会在默认日志记录设备上（通常在控制台窗口）显示一则问候消息。

### <a name="run-the-hello-task"></a>运行 Hello 任务
 使用“命令提示符窗口”  运行 MSBuild，以构造 Hello 任务并处理调用该任务的 TestBuild 目标。

##### <a name="to-run-the-hello-task"></a>运行 Hello 任务

1. 单击“开始”  ，然后单击“所有程序”  ，找到“Visual Studio Tools”  文件夹并单击“Visual Studio 命令提示符”  。

2. 在“命令提示符窗口”  中找到包含项目文件的文件夹（本例中为 D:\InlineTasks\InlineTasks\\）。 

3. 无需命令开关，键入“msbuild”  ，然后按 Enter。  默认情况下，这会生成 InlineTasks.csproj 文件并处理将调用 Hello 任务的默认目标 TestBuild。 

4. 在“命令提示符窗口”中  检查输出。 应看到此行：

    `Hello, world!`

   > [!NOTE]
   > 如果未显示问候消息，请尝试再次保存项目文件，然后运行 Hello 任务。

   通过在代码编辑器和“命令提示符窗口”  之间进行交替，可更改项目文件并快速查看结果。

## <a name="define-the-echo-task"></a>定义 Echo 任务
 创建一个会接受字符串参数并在默认日志记录设备上显示字符串的内联任务。

#### <a name="to-define-the-echo-task"></a>定义 Echo 任务

1. 在代码编辑器中，使用以下代码替换 Hello 任务和 TestBuild 目标。

   ```xml
   <UsingTask TaskName="Echo" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v4.0.dll" >
     <ParameterGroup>
       <Text Required="true" />
     </ParameterGroup>
     <Task>
       <Code Type="Fragment" Language="cs">
         Log.LogMessage(MessageImportance.High, Text);
       </Code>
     </Task>
   </UsingTask>
   <Target Name="TestBuild">
     <Echo Text="Greetings!" />
   </Target>
   ```

2. 在“命令提示符窗口”  中，无需命令开关，键入“msbuild”  ，然后按 Enter。  默认情况下，这会处理调用 Echo 任务的默认目标 TestBuild。

3. 在“命令提示符窗口”中  检查输出。 应看到此行：

    `Greetings!`

   此代码定义名为 Echo 的内联任务，且仅具有一个所需的输入参数 Text。 默认情况下，参数为 System.String 类型。 TestBuild 目标调用 Echo 任务时会设置 Text 参数的值。

## <a name="define-the-adder-task"></a>定义 Adder 任务
 创建一个会添加两个整数参数并将其总和作为 MSBuild 属性发出的内联任务。

#### <a name="to-define-the-adder-task"></a>定义 Adder 任务

1. 在代码编辑器中，使用以下代码替换 Echo 任务和 TestBuild 目标。

   ```xml
   <UsingTask TaskName="Adder" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v4.0.dll" >
     <ParameterGroup>
       <A ParameterType="System.Int32" Required="true" />
       <B ParameterType="System.Int32" Required="true" />
       <C ParameterType="System.Int32" Output="true" />
     </ParameterGroup>
     <Task>
       <Code Type="Fragment" Language="cs">
         C = A + B;
       </Code>
     </Task>
   </UsingTask>
   <Target Name="TestBuild">
     <Adder A="4" B="5">
       <Output PropertyName="Sum" TaskParameter="C" />
     </Adder>
     <Message Text="The sum is $(Sum)" Importance="High" />
   </Target>
   ```

2. 在“命令提示符窗口”  中，无需命令开关，键入“msbuild”  ，然后按 Enter。  默认情况下，这会处理调用 Echo 任务的默认目标 TestBuild。

3. 在“命令提示符窗口”中  检查输出。 应看到此行：

    `The sum is 9`

   此代码定义的内联任务名为 Adder，具有两个所需的整数输入参数（A 和 B）和一个整数输出参数 (C)。Adder 任务会添加这两个输入参数，并在输出参数中返回总和。 总和作为 MSBuild 属性 `Sum` 发出。 TestBuild 目标调用 Adder 任务时会设置输入参数的值。

## <a name="define-the-regx-task"></a>定义 RegX 任务
 创建一个内联任务，该内联任务接受项组和正则表达式，并返回其中包含与此表达式相匹配的文件内容的所有项列表。

#### <a name="to-define-the-regx-task"></a>定义 RegX 任务

1. 在代码编辑器中，使用以下代码替换 Adder 任务和 TestBuild 目标。

   ```xml
   <UsingTask TaskName="RegX" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v4.0.dll" >
     <ParameterGroup>
       <Expression Required="true" />
       <Files ParameterType="Microsoft.Build.Framework.ITaskItem[]" Required="true" />
       <Result ParameterType="Microsoft.Build.Framework.ITaskItem[]" Output="true" />
     </ParameterGroup>
     <Task>
       <Using Namespace="System.Text.RegularExpressions"/>
       <Code Type="Fragment" Language="cs">
   <![CDATA[
         if (Files.Length > 0)
         {
           Result = new TaskItem[Files.Length];
           for (int i = 0; i < Files.Length; i++)
           {
             ITaskItem item = Files[i];
             string path = item.GetMetadata("FullPath");
             using(StreamReader rdr = File.OpenText(path))
             {
               if (Regex.Match(rdr.ReadToEnd(), Expression).Success)
               {
                 Result[i] = new TaskItem(item.ItemSpec);
               }
             }
           }
         }
   ]]>
       </Code>
     </Task>
   </UsingTask>
   <Target Name="TestBuild">
     <RegX Expression="public|protected" Files="@(Compile)">
       <Output ItemName="MatchedFiles" TaskParameter="Result" />
     </RegX>
     <Message Text="Input files: @(Compile)" Importance="High" />
     <Message Text="Matched files: @(MatchedFiles)" Importance="High" />
   </Target>
   ```

2. 在“命令提示符窗口”  中，无需命令开关，键入“msbuild”  ，然后按 Enter。  默认情况下，这会处理调用 RegX 任务的默认目标 TestBuild。

3. 在“命令提示符窗口”中  检查输出。 应看到这些行：

   ```
   Input files: Form1.cs;Form1.Designer.cs;Program.cs;Properties\AssemblyInfo.cs;Properties\Resources.Designer.cs;Properties\Settings.Designer.cs
   ```

   ```
   Matched files: Form1.cs;Form1.Designer.cs;Properties\Settings.Designer.cs
   ```

   此代码定义的内联任务名为 RegX 且具有以下三个参数：

- `Expression` 是所需的字符串输入参数，其值为要匹配的正则表达式。 本示例中，表达式匹配单词“public”或“protected”。

- `Files` 是所需的项列表输入参数，其值为要在其中搜索匹配项的文件列表。 本示例中，`Files` 设置为 `Compile` 项，会列出项目源文件。

- `Result` 是一个输出参数，其值为所含内容与正则表达式匹配的文件列表。

  TestBuild 目标调用 RegX 任务时会设置输入参数的值。 RegX 任务会读取每个文件并返回与正则表达式匹配的文件列表。 此列表作为 `Result` 输出参数返回，而该输出参数作为 MSBuild 项 `MatchedFiles` 发出。

### <a name="handle-reserved-characters"></a>处理保留字符
 MSBuild 分析器将内联任务当做 XML 处理。 XML 中具有保留意义的字符（例如“\<” 和“>”）会被检测到并当作 XML 而不是 .NET 源代码进行处理。 若要在代码表达式中包含保留字符（例如 `Files.Length > 0`），请写入 `Code` 元素，其内容就可以包含在 CDATA 表达式中，如下所示：

 ```xml
<Code Type="Fragment" Language="cs">
  <![CDATA[

  // Your code goes here.

  ]]>
</Code>
```

## <a name="see-also"></a>请参阅
- [内联任务](../msbuild/msbuild-inline-tasks.md)
- [任务](../msbuild/msbuild-tasks.md)
- [目标](../msbuild/msbuild-targets.md)
