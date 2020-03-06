---
title: 如何：使用不同选项生成相同的源文件 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source files, building with different options
- MSBuild, properties
- project properties, modifying
- Hello World example [Visual Studio]
ms.assetid: d14f1212-ddd9-434f-b138-f840011b0fb2
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c31da244e5c264bb81498c6091aefce7e6318bb2
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2020
ms.locfileid: "77633936"
---
# <a name="how-to-build-the-same-source-files-with-different-options"></a>如何：使用不同选项生成相同的源文件

在生成项目时，你经常使用不同的生成选项编译相同的组件。 例如，你可以使用符号信息创建调试版本，或者使用无符号信息但启用优化来创建发布版本。 或者，可以生成项目，在某个特定平台（例如，x86 或 x64）上运行。 在所有这些情况下，大部分生成选项保持不变；只更改几个选项以控制生成配置。 利用 MSBuild，你可以使用属性和条件来创建不同的生成配置。

## <a name="use-properties-to-control-build-settings"></a>使用属性来控制生成设置

`Property` 元素定义在项目文件中多次引用的变量，如临时目录的位置，或者设置在多项配置中使用的属性的值，如调试版本和发布版本。 有关属性的详细信息，请参阅 [MSBuild 属性](../msbuild/msbuild-properties.md)。

属性可用于你的生成的配置更改，而无需更改项目文件。 `Property` 元素和 `PropertyGroup` 元素的 `Condition` 属性允许你更改属性的值。 有关 MSBuild 条件的详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。

### <a name="to-set-a-group-of-properties-that-depends-on-another-property"></a>设置一组属性（依赖于另一个属性）

- 在 `PropertyGroup` 元素中使用 `Condition` 属性，类似以下代码：

  ```xml
  <PropertyGroup Condition="'$(Flavor)'=='DEBUG'">
      <DebugType>full</DebugType>
      <Optimize>no</Optimize>
  </PropertyGroup>
  ```

### <a name="to-define-a-property-that-depends-on-another-property"></a>定义属性（依赖于另一个属性）

- 在 `Property` 元素中使用 `Condition` 属性，类似以下代码：

  ```xml
  <DebugType Condition="'$(Flavor)'=='DEBUG'">full</DebugType>
  ```

## <a name="specify-properties-on-the-command-line"></a>在命令行上指定属性

你的项目文件编写为接受多个配置后，你需要能够在生成项目时更改这些配置。 MSBuild 可以提供此功能，具体是通过允许使用 -property  或 -p  开关在命令行中指定属性。

### <a name="to-set-a-project-property-at-the-command-line"></a>在命令行中设置项目属性

- 结合使用 -property  开关与属性和属性值。 例如：

  ```cmd
  msbuild file.proj -property:Flavor=Debug
  ```

  or

  ```cmd
  Msbuild file.proj -p:Flavor=Debug
  ```

### <a name="to-specify-more-than-one-project-property-at-the-command-line"></a>在命令行上指定多个项目属性

- 多次结合使用 -property  或 -p  开关与属性和属性值，或使用一个 -property  或 -p  开关，并使用分号 (;) 分隔多个属性。 例如：

  ```cmd
  msbuild file.proj -p:Flavor=Debug;Platform=x86
  ```

  or

  ```cmd
  msbuild file.proj -p:Flavor=Debug -p:Platform=x86
  ```

  环境变量也被视为属性，并且由 MSBuild 自动合并。 有关使用环境变量的详细信息，请参阅[如何：在生成中使用环境变量](../msbuild/how-to-use-environment-variables-in-a-build.md)。

  在命令行中指定的属性值将优先于任何在项目文件中为同一属性设置的值，而项目文件中的值优先于环境变量中的值。

  你可以通过使用项目标记中的 `TreatAsLocalProperty` 属性更改此行为。 对于列出具有该特性的属性名称，在命令行上指定的属性值并不优先于项目文件中的值。 你在本主题后面找到示例。

## <a name="example"></a>示例

以下代码示例“Hello World”项目，包含两个可用于创建调试版本和发布版本的新属性组。

若要此项目的调试版本，请键入：

```cmd
msbuild consolehwcs1.proj -p:flavor=debug
```

若要此项目的零售版本，请键入：

```cmd
msbuild consolehwcs1.proj -p:flavor=retail
```

```xml
<Project DefaultTargets = "Compile"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <!-- Sets the default flavor if an environment variable called
    Flavor is not set or specified on the command line -->
    <PropertyGroup>
        <Flavor Condition="'$(Flavor)'==''">DEBUG</Flavor>
    </PropertyGroup>

    <!-- Define the DEBUG settings -->
    <PropertyGroup Condition="'$(Flavor)'=='DEBUG'">
        <DebugType>full</DebugType>
        <Optimize>no</Optimize>
    </PropertyGroup>

    <!-- Define the RETAIL settings -->
    <PropertyGroup Condition="'$(Flavor)'=='RETAIL'">
        <DebugType>pdbonly</DebugType>
        <Optimize>yes</Optimize>
    </PropertyGroup>

    <!-- Set the application name as a property -->
    <PropertyGroup>
        <appname>HelloWorldCS</appname>
    </PropertyGroup>

    <!-- Specify the inputs by type and file name -->
    <ItemGroup>
        <CSFile Include = "consolehwcs1.cs"/>
    </ItemGroup>

    <Target Name = "Compile">
        <!-- Run the Visual C# compilation using input files
        of type CSFile -->
        <CSC  Sources = "@(CSFile)"
            DebugType="$(DebugType)"
            Optimize="$(Optimize)"
            OutputAssembly="$(appname).exe" >

            <!-- Set the OutputAssembly attribute of the CSC
            task to the name of the executable file that is
            created -->
            <Output TaskParameter="OutputAssembly"
                ItemName = "EXEFile" />
        </CSC>
        <!-- Log the file name of the output file -->
        <Message Text="The output file is @(EXEFile)"/>
    </Target>
</Project>
```

## <a name="example"></a>示例

以下示例介绍如何使用 `TreatAsLocalProperty` 属性。 `Color` 属性在项目文件中的值为 `Blue`，在命令行中的值为 `Green`。 借助项目标记中的 `TreatAsLocalProperty="Color"`，命令行属性 (`Green`) 不会替代项目文件中定义的属性 (`Blue`)。

若要生成项目，请输入以下命令：

```cmd
msbuild colortest.proj -t:go -property:Color=Green
```

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"
ToolsVersion="4.0" TreatAsLocalProperty="Color">

    <PropertyGroup>
        <Color>Blue</Color>
    </PropertyGroup>

    <Target Name="go">
        <Message Text="Color: $(Color)" />
    </Target>
</Project>

<!--
  Output with TreatAsLocalProperty="Color" in project tag:
     Color: Blue

  Output without TreatAsLocalProperty="Color" in project tag:
     Color: Green
-->
```

## <a name="see-also"></a>请参阅

- [MSBuild](../msbuild/msbuild.md)
- [MSBuild 概念](../msbuild/msbuild-concepts.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [Project 元素 (MSBuild)](../msbuild/project-element-msbuild.md)
