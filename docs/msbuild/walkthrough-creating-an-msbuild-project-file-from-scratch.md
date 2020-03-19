---
title: 演练：从头开始创建 MSBuild 项目文件 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, tutorial
ms.assetid: e3acff7c-cb4e-4ae1-8be2-a871bcff847b
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5fe9f052c10f31c4db0f8bf09f273be5814ff732
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "78263131"
---
# <a name="walkthrough-create-an-msbuild-project-file-from-scratch"></a>演练：从头开始创建 MSBuild 项目文件

面向 .NET Framework 的编程语言将使用 MSBuild 项目文件来介绍并控制应用程序生成过程。 使用 Visual Studio 创建 MSBuild 项目文件时，会自动将适当的 XML 添加到该文件。 但是，你可能会发现，了解 XML 的组织方式以及如何能够更改 XML 来控制生成将非常有用。

 有关为 C++ 项目创建项目文件的信息，请参阅 [MSBuild (C++)](/cpp/build/msbuild-visual-cpp)。

 此演练演示如何只使用文本编辑器以增量方式创建基本项目文件。 演练采用以下步骤：

1. 创建最小的应用程序源文件。

2. 创建最小的 MSBuild 项目文件。

3. 扩展 PATH 环境变量以包括 MSBuild。

4. 使用项目文件生成应用程序。

5. 添加属性以控制生成。

6. 通过更改属性值来控制生成。

7. 将目标添加到生成。

8. 通过指定目标来控制生成。

9. 以增量方式生成。

此演练演示如何在命令提示符下生成项目并检查结果。 有关 MSBuild 以及如何在命令提示符下运行 MSBuild 的详细信息，请参阅[演练：使用 MSBuild](../msbuild/walkthrough-using-msbuild.md)。

若要完成本演练，必须安装 .NET Framework（版本 2.0、3.5、4.0、4.5 或更高版本），因为它包含演练所需的 MSBuild 和 Visual C# 编译器。

## <a name="create-a-minimal-application"></a>创建最小的应用程序

 本部分演示如何使用文本编辑器创建最小的 C# 应用程序源文件。

1. 在命令提示符下，浏览到要在其中创建应用程序的文件夹，例如，\My Documents *\\* 或 \Desktop *\\* 。

2. 键入“md HelloWorld”  创建名为“\HelloWorld *”\\* 的子文件夹。

3. 键入 **cd HelloWorld** 切换到该新文件夹。

4. 启动记事本或其他文本编辑器，然后键入以下代码。

    ```csharp
    using System;

    class HelloWorld
    {
        static void Main()
        {
    #if DebugConfig
            Console.WriteLine("WE ARE IN THE DEBUG CONFIGURATION");
    #endif

            Console.WriteLine("Hello, world!");
        }
    }
    ```

5. 保存此源代码文件，并将其命名为“Helloworld.cs”  。

6. 在命令提示符下，键入 **csc helloworld.cs** 来生成应用程序。

7. 在命令提示符下，键入 **helloworld** 测试应用程序。

     显示的消息应为 **Hello, world!** 。

8. 在命令提示符下，键入 **del helloworld.exe** 删除应用程序。

## <a name="create-a-minimal-msbuild-project-file"></a>创建最小的 MSBuild 项目文件

 既然有了最小的应用程序源文件，你就可以创建最小的项目文件来生成应用程序。 此项目文件包含以下元素：

- 必需的根 `Project` 节点。

- 用于包含项元素的 `ItemGroup` 节点。

- 引用应用程序源文件的项元素。

- 一个 `Target` 节点，用于包含生成应用程序所需的任务。

- 一个 `Task` 元素，用于启动 Visual C# 编译器以生成应用程序。

### <a name="to-create-a-minimal-msbuild-project-file"></a>创建最小的 MSBuild 项目文件

1. 在文本编辑器中，用以下两行替换现有文本：

    ```xml
    <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    </Project>
    ```

2. 插入此 `ItemGroup` 节点，作为 `Project` 节点的子元素：

    ```xml
    <ItemGroup>
      <Compile Include="helloworld.cs" />
    </ItemGroup>
    ```

     请注意，此 `ItemGroup` 已包含一个项元素。

3. 添加一个 `Target` 节点，作为 `Project` 节点的子元素。 将该节点命名为 `Build`。

    ```xml
    <Target Name="Build">
    </Target>
    ```

4. 插入此 task 元素，作为 `Target` 节点的子元素：

    ```xml
    <Csc Sources="@(Compile)"/>
    ```

5. 保存此项目文件，并将其命名为“Helloworld.csproj”  。

你的最小项目文件应类似于以下代码：

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <ItemGroup>
    <Compile Include="helloworld.cs" />
  </ItemGroup>
  <Target Name="Build">
    <Csc Sources="@(Compile)"/>  
  </Target>
</Project>
```

Build 目标中的任务按顺序执行。 在本例中，Visual C# 编译器 `Csc` 任务是唯一的任务。 它需要编译一系列源文件，这一系列文件由 `Compile` 项的值指定。 `Compile` 项只引用一个源文件，即 Helloworld.cs  。

> [!NOTE]
> 在项元素中，可以使用星号通配符 (\*) 来引用文件扩展名为 .cs  的所有文件，如下所示：
>
> ```xml
> <Compile Include="*.cs" />
> ```

## <a name="extend-the-path-to-include-msbuild"></a>扩展路径以包括 MSBuild

必须先扩展 PATH 环境变量以包括 .NET Framework 文件夹，然后才能访问 MSBuild。

从 Visual Studio 2013 开始，可以在 MSBuild 文件夹（32 位操作系统上的 %ProgramFiles%\MSBuild 或 64 位操作系统上的 %ProgramFiles(x86)%\MSBuild）中查找 MSBuild.exe    。

在命令提示符处，键入 **set PATH=%PATH%;%ProgramFiles%\MSBuild** 或 **set PATH=%PATH%;%ProgramFiles(x86)%\MSBuild**。

或者，如果安装了 Visual Studio，则可以使用 Visual Studio 开发人员命令提示，其中具有包含 MSBuild 文件夹的路径   。

## <a name="build-the-application"></a>生成应用程序

 现在，为了生成应用程序，请使用刚刚创建的项目文件。

1. 在命令提示符处，键入 msbuild helloworld.csproj -t:Build  。

     此操作将调用 Visual C# 编译器来创建 Helloworld 应用程序，从而生成 Helloworld 项目文件的 Build 目标。

2. 键入 **helloworld** 测试应用程序。

     显示的消息应为 **Hello, world!** 。

> [!NOTE]
> 可以通过提高详细信息级别来查看有关生成的更多详细级别。 要将详细级别设置为“详细”，请在命令提示符下键入命令：
>
> **msbuild helloworld.csproj -t:Build -verbosity:detailed**

## <a name="add-build-properties"></a>添加生成属性

 可以将生成属性添加到项目文件中，从而进一步控制生成。 现在添加以下属性：

- 一个 `AssemblyName` 属性，用于指定应用程序的名称。

- 一个 `OutputPath` 属性，用于指定要包含应用程序的文件夹。

### <a name="to-add-build-properties"></a>添加生成属性

1. 在命令提示符下，键入 **del helloworld.exe** 删除现有应用程序。

2. 在项目文件中，插入此 `PropertyGroup` 元素，置于起始 `Project` 元素的后面：

    ```xml
    <PropertyGroup>
      <AssemblyName>MSBuildSample</AssemblyName>
      <OutputPath>Bin\</OutputPath>
    </PropertyGroup>
    ```

3. 将此任务添加到 Build 目标，置于 `Csc` 任务的前面：

    ```xml
    <MakeDir Directories="$(OutputPath)"      Condition="!Exists('$(OutputPath)')" />
    ```

     `MakeDir` 任务将创建一个由 `OutputPath` 属性命名的文件夹，前提是当前不存在具有该名称的文件夹。

4. 将此 `OutputAssembly` 特性添加到 `Csc` 任务：

    ```xml
    <Csc Sources="@(Compile)" OutputAssembly="$(OutputPath)$(AssemblyName).exe" />
    ```

     这将指示 Visual C# 编译器生成由 `AssemblyName` 属性命名的程序集，并将其放在由 `OutputPath` 属性命名的文件夹中。

5. 保存所做更改。

你的项目文件现在应类似于以下代码：

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <AssemblyName>MSBuildSample</AssemblyName>
    <OutputPath>Bin\</OutputPath>
  </PropertyGroup>
  <ItemGroup>
    <Compile Include="helloworld.cs" />
  </ItemGroup>
  <Target Name="Build">
    <MakeDir Directories="$(OutputPath)" Condition="!Exists('$(OutputPath)')" />
    <Csc Sources="@(Compile)" OutputAssembly="$(OutputPath)$(AssemblyName).exe" />
  </Target>
</Project>
```

> [!NOTE]
> 在 \\ 元素中指定文件夹名称时，建议在文件夹名称的末尾添加反斜杠 (`OutputPath`) 路径分隔符，而不是将其添加到 `OutputAssembly` 任务的 `Csc` 属性中。 因此，
>
> `<OutputPath>Bin\</OutputPath>`
>
> `OutputAssembly=="$(OutputPath)$(AssemblyName).exe" />`
>
> 优于
>
> `<OutputPath>Bin</OutputPath>`
>
> `OutputAssembly=="$(OutputPath)\$(AssemblyName).exe" />`

## <a name="test-the-build-properties"></a>测试生成属性

 现在即可使用项目文件来生成应用程序，在该项目文件中，你使用了生成属性来指定输出文件夹和应用程序名称。

1. 在命令提示符处，键入 msbuild helloworld.csproj -t:Build  。

     这将创建“\Bin *”\\* 文件夹，然后调用 Visual C# 编译器创建 MSBuildSample  应用程序，并将其放在“\Bin *”\\* 文件夹中。

2. 要验证是否已创建“\Bin *”\\* 文件夹，以及该文件夹是否包含 MSBuildSample  应用程序，请键入“dir Bin”  。

3. 键入 **Bin\MSBuildSample** 测试应用程序。

     显示的消息应为 **Hello, world!** 。

## <a name="add-build-targets"></a>添加生成目标

 接下来，向项目文件中另外添加两个目标，如下所示：

- 一个用于删除旧文件的 Clean 目标。

- 一个 Rebuild 目标，该目标使用 `DependsOnTargets` 特性，强制使 Clean 任务在 Build 任务之前运行。

既然有多个目标，就可以将 Build 目标设置为默认目标。

### <a name="to-add-build-targets"></a>添加生成目标

1. 在项目文件中添加以下两个目标，置于 Build 目标的后面：

    ```xml
    <Target Name="Clean" >
      <Delete Files="$(OutputPath)$(AssemblyName).exe" />
    </Target>
    <Target Name="Rebuild" DependsOnTargets="Clean;Build" />
    ```

     Clean 目标调用 Delete 任务来删除应用程序。 在 Clean 目标和 Build 目标均已运行之前，Rebuild 目标不会运行。 尽管 Rebuild 目标没有任务，但它可使 Clean 目标在 Build 目标之前运行。

2. 将此 `DefaultTargets` 特性添加到起始 `Project` 元素：

    ```xml
    <Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    ```

     这会将 Build 目标设置为默认目标。

你的项目文件现在应类似于以下代码：

```xml
<Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <AssemblyName>MSBuildSample</AssemblyName>
    <OutputPath>Bin\</OutputPath>
  </PropertyGroup>
  <ItemGroup>
    <Compile Include="helloworld.cs" />
  </ItemGroup>
  <Target Name="Build">
    <MakeDir Directories="$(OutputPath)" Condition="!Exists('$(OutputPath)')" />
    <Csc Sources="@(Compile)" OutputAssembly="$(OutputPath)$(AssemblyName).exe" />
  </Target>
  <Target Name="Clean" >
    <Delete Files="$(OutputPath)$(AssemblyName).exe" />
  </Target>
  <Target Name="Rebuild" DependsOnTargets="Clean;Build" />
</Project>
```

## <a name="test-the-build-targets"></a>测试生成目标

 可以执行新的生成目标来测试项目文件的以下功能：

- 生成默认生成。

- 在命令提示符下设置应用程序名称。

- 在生成其他应用程序之前删除应用程序。

- 删除应用程序，而不生成其他应用程序。

### <a name="to-test-the-build-targets"></a>测试生成目标

1. 在命令提示符处，键入msbuild helloworld.csproj -p:AssemblyName=Greetings  。

     由于未使用 -t  开关显式设置目标，因此 MSBuild 运行默认 Build 目标。 -p  开关替代 `AssemblyName` 属性，并为它指定新值 `Greetings`。 这将导致在“\Bin *”* *文件夹中创建一个新应用程序 Greetings.exe\\* 。

2. 要验证“\Bin *”\\* 文件夹是否同时包含 MSBuildSample  应用程序和新的 Greetings  应用程序，请键入“dir Bin”  。

3. 键入 **Bin\Greetings** 测试 Greetings 应用程序。

     显示的消息应为 **Hello, world!** 。

4. 通过键入 msbuild helloworld.csproj -t:clean  ，删除 MSBuildSample 应用程序。

     这将运行 Clean 任务，以删除具有默认 `AssemblyName` 属性值 `MSBuildSample` 的应用程序。

5. 通过键入 msbuild helloworld.csproj -t:clean -p:AssemblyName=Greetings  ，删除 Greetings 应用程序。

     这将运行 Clean 任务，以删除具有指定 **AssemblyName** 属性值 `Greetings` 的应用程序。

6. 要验证“\Bin *”\\* 文件夹现在是否为空，请键入“dir Bin”  。

7. 键入 **msbuild**。

     尽管未指定项目文件，但 MSBuild 会生成 helloworld.csproj  文件，因为当前文件夹中只有一个项目文件。 这将导致在“\Bin *”* *文件夹中创建 MSBuildSample\\* 应用程序。

     要验证“\Bin *”\\* 文件夹是否包含 MSBuildSample  应用程序，请键入“dir Bin”  。

## <a name="build-incrementally"></a>增量生成

 可以指示 MSBuild 仅在目标所依赖的源文件或目标文件发生更改时才生成目标。 MSBuild 使用文件的时间戳来确定文件是否已更改。

### <a name="to-build-incrementally"></a>以增量方式生成

1. 在项目文件中，将以下特性添加到起始 Build 目标：

    ```xml
    Inputs="@(Compile)" Outputs="$(OutputPath)$(AssemblyName).exe"
    ```

     它指定 Build 目标依赖于 `Compile` 项组中指定的输入文件，并且输出目标为应用程序文件。

     生成的 Build 目标应类似于以下代码：

    ```xml
    <Target Name="Build" Inputs="@(Compile)" Outputs="$(OutputPath)$(AssemblyName).exe">
      <MakeDir Directories="$(OutputPath)" Condition="!Exists('$(OutputPath)')" />
      <Csc Sources="@(Compile)" OutputAssembly="$(OutputPath)$(AssemblyName).exe" />
    </Target>
    ```

2. 在命令提示符处，键入 msbuild -v:d  ，以测试 Build 目标。

     请记住，helloworld.csproj  是默认项目文件，并且 Build 为默认目标。

     -v:d  开关指定了生成流程的详细说明。

     此时应显示以下各行：

     **正在跳过目标“Build”，因为所有输出文件相对于输入文件而言都是最新的**

     **输入文件：HelloWorld.cs**

     **输出文件：BinMSBuildSample.exe**

     MSBuild 将跳过 Build 目标，原因是自上次生成应用程序以来没有任何源文件发生更改。

## <a name="c-example"></a>C# 示例

下面的示例演示一个项目文件，该项目文件编译 C# 应用程序并记录包含输出文件名的消息。

### <a name="code"></a>代码

```xml
<Project DefaultTargets = "Compile"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >

    <!-- Set the application name as a property -->
    <PropertyGroup>
        <appname>HelloWorldCS</appname>
    </PropertyGroup>

    <!-- Specify the inputs by type and file name -->
    <ItemGroup>
        <CSFile Include = "consolehwcs1.cs"/>
    </ItemGroup>

    <Target Name = "Compile">
        <!-- Run the Visual C# compilation using input files of type CSFile -->
        <CSC
            Sources = "@(CSFile)"
            OutputAssembly = "$(appname).exe">
            <!-- Set the OutputAssembly attribute of the CSC task
            to the name of the executable file that is created -->
            <Output
                TaskParameter = "OutputAssembly"
                ItemName = "EXEFile" />
        </CSC>
        <!-- Log the file name of the output file -->
        <Message Text="The output file is @(EXEFile)"/>
    </Target>
</Project>
```

## <a name="visual-basic-example"></a>Visual Basic 示例

下面的示例演示一个项目文件，该项目文件编译 Visual Basic 应用程序并记录包含输出文件名的消息。

### <a name="code"></a>代码

```xml
<Project DefaultTargets = "Compile"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >

    <!-- Set the application name as a property -->
    <PropertyGroup>
        <appname>HelloWorldVB</appname>
    </PropertyGroup>

    <!-- Specify the inputs by type and file name -->
    <ItemGroup>
        <VBFile Include = "consolehwvb1.vb"/>
    </ItemGroup>

    <Target Name = "Compile">
        <!-- Run the Visual Basic compilation using input files of type VBFile -->
        <VBC
            Sources = "@(VBFile)"
            OutputAssembly= "$(appname).exe">
            <!-- Set the OutputAssembly attribute of the VBC task
            to the name of the executable file that is created -->
            <Output
                TaskParameter = "OutputAssembly"
                ItemName = "EXEFile" />
        </VBC>
        <!-- Log the file name of the output file -->
        <Message Text="The output file is @(EXEFile)"/>
    </Target>
</Project>
```

## <a name="whats-next"></a>后续步骤

 Visual Studio 能够自动执行本演练中演示的大部分工作。 若要了解如何使用 Visual Studio 来创建、编辑、生成和测试 MSBuild 项目文件，请参阅[演练：使用 MSBuild](../msbuild/walkthrough-using-msbuild.md)。

## <a name="see-also"></a>另请参阅

- [MSBuild 概述](../msbuild/msbuild.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)
