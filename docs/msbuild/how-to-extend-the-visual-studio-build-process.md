---
title: 扩展生成过程
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, overriding predefined targets
- MSBuild, overriding DependsOn properties
- MSBuild, extending Visual Studio builds
- MSBuild, DependsOn properties
ms.assetid: cb077613-4a59-41b7-96ec-d8516689163c
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ac3bebc0a64f814e71e7b5ab30282a70fd7eb85e
ms.sourcegitcommit: d293c0e3e9cc71bd4117b6dfd22990d52964addc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/10/2020
ms.locfileid: "88041033"
---
# <a name="how-to-extend-the-visual-studio-build-process"></a>如何：扩展 Visual Studio 生成过程

Visual Studio 生成过程由导入到项目文件中的一系列 MSBuild .targets  文件定义。 可扩展其中一个导入文件 Microsoft.Common.targets，以便在生成过程中的几个点上运行自定义任务  。 本文介绍两种可用于扩展 Visual Studio 生成过程的方法：

- 重写公共目标中定义的特定预定义目标（Microsoft.Common.targets 或其导入的文件）  。

- 重写公共目标中定义的“DependsOn”属性。

## <a name="override-predefined-targets"></a>重写预定义目标

公共目标包含一组预定义的空目标，在生成过程中某些主目标的前后会调用这些空目标。 例如，MSBuild 会在主 `CoreBuild` 目标之前调用 `BeforeBuild` 目标，在 `CoreBuild` 目标之后调用 `AfterBuild` 目标。 公共目标中的空目标默认不执行任何操作，但可通过定义导入公共目标的项目文件中所需的目标，重写这些空目标的默认行为。 通过重写预定义目标，可以使用 MSBuild 任务，更好地控制生成过程。

> [!NOTE]
> SDK 类型的项目在项目文件的最后一行后会隐式导入目标**。 这意味着，除非根据[如何：使用 MSBuild 项目 SDK](how-to-use-project-sdk.md) 中所述的方法手动指定导入，否则无法重写默认目标。

#### <a name="to-override-a-predefined-target"></a>重写预定义的目标

1. 标识公共目标中需要重写的预定义目标。 请参阅下表，了解可安全重写的目标的完整列表。

2. 在项目文件末尾（紧接在 `</Project>` 标记之前）定义一个或多个目标。 例如：

    ```xml
    <Project>
        ...
        <Target Name="BeforeBuild">
            <!-- Insert tasks to run before build here -->
        </Target>
        <Target Name="AfterBuild">
            <!-- Insert tasks to run after build here -->
        </Target>
    </Project>
    ```

3. 生成项目文件。

下表显示公共目标中可以安全重写的所有目标。

|目标名称|说明|
|-----------------|-----------------|
|`BeforeCompile`, `AfterCompile`|插入到这些目标之一中的任务，在完成内核编译之前或之后运行。 大多数自定义均在这两个目标之一中完成。|
|`BeforeBuild`, `AfterBuild`|插入到这些目标之一中的任务，在生成中所有其他任务之前或之后运行。 注意：`BeforeBuild` 和 `AfterBuild` 目标已在大多数项目文件的注释末尾定义，使你能够轻松向项目文件添加预生成和生成后事件****。|
|`BeforeRebuild`, `AfterRebuild`|插入到这些目标之一中的任务，在调用内核重新生成功能之前或之后运行。 Microsoft.Common.targets 中的目标执行顺序是：`BeforeRebuild`、`Clean`、`Build`、`AfterRebuild`。|
|`BeforeClean`, `AfterClean`|插入到这些目标之一中的任务，在调用内核清理功能之前或之后运行。|
|`BeforePublish`, `AfterPublish`|插入到这些目标之一中的任务，在调用内核发布功能之前或之后运行。|
|`BeforeResolveReferences`，`AfterResolveReferences`|插入到这些目标之一中的任务，在解析程序集引用之前或之后运行。|
|`BeforeResGen`，`AfterResGen`|插入到这些目标之一中的任务，在生成资源之前或之后运行。|

## <a name="example-aftertargets-and-beforetargets"></a>示例：AfterTargets 和 BeforeTargets

下面的示例演示如何使用 `AfterTargets` 属性添加对输出文件执行某些操作的自定义目标。 在这种情况下，它会将输出文件复制到“CustomOutput”的新文件夹中。  该示例还演示如何使用 `BeforeTargets` 属性并指定自定义清理操作在目标 `CoreClean` 之前运行，用 `CustomClean` 目标清理由自定义生成操作创建的文件。

```xml
<Project Sdk="Microsoft.NET.Sdk">

<PropertyGroup>
   <TargetFramework>netcoreapp3.1</TargetFramework>
   <_OutputCopyLocation>$(OutputPath)..\..\CustomOutput\</_OutputCopyLocation>
</PropertyGroup>

<Target Name="CustomAfterBuild" AfterTargets="Build">
  <ItemGroup>
    <_FilesToCopy Include="$(OutputPath)**\*"/>
  </ItemGroup>
  <Message Text="_FilesToCopy: @(_FilesToCopy)" Importance="high"/>

  <Message Text="DestFiles:
      @(_FilesToCopy->'$(_OutputCopyLocation)%(RecursiveDir)%(Filename)%(Extension)')"/>

  <Copy SourceFiles="@(_FilesToCopy)"
        DestinationFiles=
        "@(_FilesToCopy->'$(_OutputCopyLocation)%(RecursiveDir)%(Filename)%(Extension)')"/>
  </Target>

  <Target Name="CustomClean" BeforeTargets="CoreClean">
    <Message Text="Inside Custom Clean" Importance="high"/>
    <ItemGroup>
      <_CustomFilesToDelete Include="$(_OutputCopyLocation)**\*"/>
    </ItemGroup>
    <Delete Files='@(_CustomFilesToDelete)'/>
  </Target>
</Project>
```

> [!WARNING]
> 请确保使用其他名称，该名称要与上一节中表中列出的预定义目标不同（例如，我们在此处命名自定义生成目标 `CustomAfterBuild`，而不是 `AfterBuild`），因为这些预定义的目标会被 SDK 导入覆盖，SDK 导入也定义这些目标。 你看不到覆盖这些目标的目标文件的导入，但在使用引用 SDK 的 `Sdk` 属性方法时，该文件将隐式添加到项目文件的末尾。

## <a name="override-dependson-properties"></a>重写 DependsOn 属性

重写预定义的目标是一种用于扩展生成过程的简单方法，但由于 MSBuild 按顺序计算目标的定义，任何方法都无法阻止已导入你的项目的另一个项目重写你已重写的目标。 因此，例如，在导入所有其他项目后，会在生成过程中使用项目文件中定义的最后一个 `AfterBuild` 目标。

通过重写在全部公共目标的 `DependsOnTargets` 特性中使用的“DependsOn”属性，可防止目标被意外重写。 例如，`Build` 目标包含 `"$(BuildDependsOn)"` 的 `DependsOnTargets` 属性值。 请注意以下几点：

```xml
<Target Name="Build" DependsOnTargets="$(BuildDependsOn)"/>
```

这一段 XML 指示运行 `Build` 目标之前，必须首先运行 `BuildDependsOn` 属性中指定的所有目标。 `BuildDependsOn` 属性的定义如下：

```xml
<PropertyGroup>
    <BuildDependsOn>
        BeforeBuild;
        CoreBuild;
        AfterBuild
    </BuildDependsOn>
</PropertyGroup>
```

通过在项目文件末尾声明另一个名为 `BuildDependsOn` 的属性，可以重写此属性值。 通过在新属性中包括以前的 `BuildDependsOn` 属性，可以将新的目标添加到目标列表的开头和结尾。 例如：

```xml
<PropertyGroup>
    <BuildDependsOn>
        MyCustomTarget1;
        $(BuildDependsOn);
        MyCustomTarget2
    </BuildDependsOn>
</PropertyGroup>

<Target Name="MyCustomTarget1">
    <Message Text="Running MyCustomTarget1..."/>
</Target>
<Target Name="MyCustomTarget2">
    <Message Text="Running MyCustomTarget2..."/>
</Target>
```

导入你的项目文件的项目可以在不覆盖已实现的自定义的情况下重写这些属性。

#### <a name="to-override-a-dependson-property"></a>重写 DependsOn 属性

1. 标识公共目标中需要重写的预定义 DependsOn 属性。 请参阅下表，获取经常重写的 DependsOn 属性列表。

2. 在项目文件末尾定义一个或多个属性的另一个实例。 在新属性中包括原始属性，例如 `$(BuildDependsOn)`。

3. 在属性定义之前或之后定义自定义目标。

4. 生成项目文件。

### <a name="commonly-overridden-dependson-properties"></a>经常重写的 DependsOn 属性

|属性名称|说明|
|-------------------|-----------------|
|`BuildDependsOn`|在要在整个生成过程之前或之后插入自定义目标的情况下，要重写的属性。|
|`CleanDependsOn`|在要从自定义生成过程中清理输出的情况下，要重写的属性。|
|`CompileDependsOn`|在要在编译步骤之前或之后插入自定义过程的情况下，要重写的属性。|

## <a name="example-builddependson-and-cleandependson"></a>示例：BuildDependsOn and CleanDependsOn

下面的示例类似于 `BeforeTargets` 和 `AfterTargets` 示例，但演示了如何实现类似的功能。 它通过使用 `BuildDependsOn` 来添加你自己的任务 `CustomAfterBuild` 以在生成后复制输出文件，并使用 `CleanDependsOn` 添加相应的 `CustomClean` 任务，从而扩展生成。  

在此示例中，这是一个 SDK 样式项目。 如本文前面有关 SDK 样式项目的注释中所述，必须使用手动导入方法，而不是 Visual Studio 生成项目文件时使用的 `Sdk` 属性。

```xml
<Project>
<Import Project="Sdk.props" Sdk="Microsoft.NET.Sdk" />

<PropertyGroup>
   <TargetFramework>netcoreapp3.1</TargetFramework>
</PropertyGroup>

<Import Project="Sdk.targets" Sdk="Microsoft.NET.Sdk" />

<PropertyGroup>
   <BuildDependsOn>
      $(BuildDependsOn);CustomAfterBuild
    </BuildDependsOn>

    <CleanDependsOn>
      $(CleanDependsOn);CustomClean
    </CleanDependsOn>

    <_OutputCopyLocation>$(OutputPath)..\..\CustomOutput\</_OutputCopyLocation>
  </PropertyGroup>

<Target Name="CustomAfterBuild">
  <ItemGroup>
    <_FilesToCopy Include="$(OutputPath)**\*"/>
  </ItemGroup>
  <Message Text="_FilesToCopy: @(_FilesToCopy)" Importance="high"/>

  <Message Text="DestFiles:
      @(_FilesToCopy->'$(_OutputCopyLocation)%(RecursiveDir)%(Filename)%(Extension)')"/>

  <Copy SourceFiles="@(_FilesToCopy)"
        DestinationFiles=
        "@(_FilesToCopy->'$(_OutputCopyLocation)%(RecursiveDir)%(Filename)%(Extension)')"/>
  </Target>

  <Target Name="CustomClean">
    <Message Text="Inside Custom Clean" Importance="high"/>
    <ItemGroup>
      <_CustomFilesToDelete Include="$(_OutputCopyLocation)**\*"/>
    </ItemGroup>
    <Delete Files='@(_CustomFilesToDelete)'/>
  </Target>
</Project>
```

元素的顺序非常重要。 导入标准 SDK 目标文件后，必须出现 `BuildDependsOn` 和 `CleanDependsOn` 元素。

## <a name="see-also"></a>另请参阅

- [Visual Studio 集成](../msbuild/visual-studio-integration-msbuild.md)
- [MSBuild 概念](../msbuild/msbuild-concepts.md)
- [.targets 文件](../msbuild/msbuild-dot-targets-files.md)
