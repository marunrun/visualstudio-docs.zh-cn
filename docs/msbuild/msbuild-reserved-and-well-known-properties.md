---
title: MSBuild 保留属性和已知属性 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, reserved properties
ms.assetid: 99333e61-83c9-4804-84e3-eda297c2478d
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5c3d97185446560343b36b22f73e0b320b5a28d6
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85289217"
---
# <a name="msbuild-reserved-and-well-known-properties"></a>MSBuild 保留属性和已知属性

MSBuild 提供了一组预定义的属性，这些属性存储项目文件和 MSBuild 二进制文件的相关信息。 这些属性的计算方式与其他 MSBuild 属性相同。 例如，要使用 `MSBuildProjectFile` 属性，应键入 `$(MSBuildProjectFile)`。

 MSBuild 使用下表中的值预定义保留的属性和已知的属性。 无法重写保留的属性，但可以使用名称相同的环境属性、全局属性或已在项目文件中声明的属性重写已知的属性。

## <a name="reserved-and-well-known-properties"></a>保留属性和已知属性

此部分中的表显示了 MSBuild 预定义属性。 表中的示例列与以下示例项目文件相关（假定位于 `C:\Source\Repos\ConsoleApp1\ConsoleApp1`），并显示了这些属性在以下情况下的值：在项目文件中被访问时，以及在没有特殊命令行选项的情况下调用 MSBuild 时，同时安装了 Visual Studio 2019 版本 16.7 的预览内部版本。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>
  </PropertyGroup>
</Project>
```

| Property | 保留或已知 | 描述 | 示例 |
|----------------------------------|------------------------| - | - |
| `MSBuildBinPath` | 保留 | 当前正在使用的 MSBuild 二进制文件所在文件夹的绝对路径（例如，C:\Windows\Microsoft.Net\Framework\\\<versionNumber>）。 如果必须引用 MSBuild 目录中的文件，此属性将非常有用。<br /><br /> 不要在此属性上添加最终反斜杠。 | `C:\Program Files (x86)\Microsoft Visual Studio\2019\Preview\MSBuild\Current\Bin` |
| `MSBuildExtensionsPath` | 已知 | 在 .NET Framework 4 中引入：`MSBuildExtensionsPath` 和 `MSBuildExtensionsPath32` 的默认值之间没有差异。 你可以设置环境变量 `MSBUILDLEGACYEXTENSIONSPATH` 为非 null 值，以启用早期版本中的 `MSBuildExtensionsPath`的默认值的行为。<br /><br /> 在 .NET Framework 3.5 和较早的版本中，根据当前进程的位数，`MSBuildExtensionsPath` 的默认值指向位于 \Program Files\\ 或 \Program Files (x86) 文件夹下的 MSBuild 子文件夹路径 。 例如，对于在 64 位计算机上的 32 位进程，此属性指向 \Program Files (x86) 文件夹。 对于在 64 位计算机上的 64 位进程，此属性指向 \Program Files 文件夹。<br /><br /> 不要在此属性上添加最终反斜杠。<br /><br /> 此位置用于存放自定义目标文件。 例如，目标文件可能安装在 \Program Files\MSBuild\MyFiles\Northwind.targets 中，然后使用此 XML 代码导入到项目文件中：<br /><br /> `<Import Project="$(MSBuildExtensionsPath)\MyFiles\Northwind.targets"/>` | `C:\Program Files (x86)\Microsoft Visual Studio\2019\Preview\MSBuild`|
| `MSBuildExtensionsPath32` | 已知 | 位于 \Program Files 或 \Program Files (x86) 文件夹下的 MSBuild 子文件夹的路径。 此路径始终指向 32 位计算机上的 32 位 \Program Files (x86) 文件夹和 64 位计算机上的 \Program Files 。 另请参见 `MSBuildExtensionsPath` 和 `MSBuildExtensionsPath64`。<br /><br /> 不要在此属性上添加最终反斜杠。 | `C:\Program Files (x86)\Microsoft Visual Studio\2019\Preview\MSBuild`|
| `MSBuildExtensionsPath64` | 已知 | 位于 \Program Files 文件夹下的 MSBuild 子文件夹的路径。 对于 64 位计算机，此路径始终指向 \Program Files 文件夹。 对于 32 位计算机，此路径为空。 另请参见 `MSBuildExtensionsPath` 和 `MSBuildExtensionsPath32`。<br /><br /> 不要在此属性上添加最终反斜杠。 | `C:\Program Files\MSBuild`|
| `MSBuildInteractive` | 保留 | `true`，如果 MSBuild 以交互方式运行，则允许用户输入。 此设置由 `-interactive` 命令行选项控制。 | `false` |
| `MSBuildLastTaskResult` | 保留 | `true`，如果前一项任务完成没有出现任何错误（即使有警告）；否则如果前一项任务出现错误，则为 `false`。 通常，当任务中出现错误时，错误会发生在项目的最后。 因此，此属性的值决不会是 `false`，但以下情况除外：<br /><br /> - [Task 元素 (MSBuild)](../msbuild/task-element-msbuild.md) 的 `ContinueOnError` 属性设置为 `WarnAndContinue`（或 `true`）或 `ErrorAndContinue` 时。<br /><br /> - `Target` 将 [OnError 元素 (MSBuild)](../msbuild/onerror-element-msbuild.md) 作为子元素时。 | `true` |
| `MSBuildNodeCount` | 保留 | 生成过程中使用的并发进程的最大数目。 这是在命令行中为 -maxcpucount 指定的值。 如果指定了 -maxcpucount 但没有指定值，`MSBuildNodeCount` 会指定计算机中的处理器数。 有关详细信息，请参阅[命令行参考](../msbuild/msbuild-command-line-reference.md)和[并行生成多个项目](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)。 | 1 |
| `MSBuildProgramFiles32` | 保留 | 32 位程序文件夹的位置；例如，C:\Program Files (x86)。<br /><br /> 不要在此属性上添加最终反斜杠。 | `C:\Program Files (x86)`|
| `MSBuildProjectDefaultTargets` | 保留 | `DefaultTargets` 元素的 `Project` 特性中指定的目标的完整列表。 例如，下面的 `Project` 元素的 `MSBuildDefaultTargets` 属性值为 `A;B;C`：<br /><br /> `<Project DefaultTargets="A;B;C" >` | `Build`|
| `MSBuildProjectDirectory` | 保留 | 项目文件所在目录的绝对路径，例如，C:\MyCompany\MyProduct。<br /><br /> 不要在此属性上添加最终反斜杠。 | `C:\Source\Repos\ConsoleApp1\ConsoleApp1` |
| `MSBuildProjectDirectoryNoRoot` | 保留 | `MSBuildProjectDirectory` 属性的值，但不包括根驱动器。<br /><br /> 不要在此属性上添加最终反斜杠。 | `Source\Repos\ConsoleApp1\ConsoleApp1`|
| `MSBuildProjectExtension` | 保留 | 项目文件的文件扩展名（包括点号）；例如，.proj。 | `.csproj`|
| `MSBuildProjectFile` | 保留 | 项目文件的完整文件名（包括文件扩展名）；例如，MyApp.proj。 | `ConsoleApp1.csproj`|
| `MSBuildProjectFullPath` | 保留 | 项目文件的绝对路径和完整文件名（包括文件扩展名）；例如，C:\MyCompany\MyProduct\MyApp.proj。 | `c:\Source\Repos\ConsoleApp1\ConsoleApp1\ConsoleApp1.csproj`|
| `MSBuildProjectName` | 保留 | 项目文件的文件名（不包括文件扩展名）；例如，MyApp。 | `ConsoleApp1` |
| `MSBuildRuntimeType` | 保留 | 当前正在执行的运行时类型。 在 MSBuild 15 中引入。 可能未定义值（MSBuild 15 之前），`Full` 指示 MSBuild 在桌面 .NET Framework 上运行，`Core` 指示 MSBuild 在 .NET Core 上运行（例如在 `dotnet build` 中），`Mono` 指示 MSBuild 在 Mono 上运行。 | `Full` |
| `MSBuildStartupDirectory` | 保留 | 在其中调用 MSBuild 的文件夹的绝对路径。 使用此属性，无需在每个目录中都创建 \<dirs>.proj 文件，就可以在项目树中的某个特定点下生成所有内容。 而你只有一个项目，例如 c:\traversal.proj（如此处所示）：<br /><br /> `<Project ...>     <ItemGroup>         <ProjectFiles              Include="$            (MSBuildStartupDirectory)            **\*.csproj"/>     </ItemGroup>     <Target Name="build">         <MSBuild             Projects="@(ProjectFiles)"/>     </Target> </Project>`<br /><br /> 若要在该树中的任意一点生成，请键入：<br /><br /> `msbuild c:\traversal.proj`<br /><br /> 不要在此属性上添加最终反斜杠。 | `c:\Source\Repos\ConsoleApp1` |
| `MSBuildThisFile` | 保留 | `MSBuildThisFileFullPath` 的文件名和文件扩展名部分。 | `ConsoleApp1.csproj` |
| `MSBuildThisFileDirectory` | 保留 | `MSBuildThisFileFullPath` 的目录部分。<br /><br /> 将最终反斜杠包括在路径中。 | `c:\Source\Repos\ConsoleApp1\ConsoleApp1\` |
| `MSBuildThisFileDirectoryNoRoot` | 保留 | `MSBuildThisFileFullPath` 的目录部分不包括根驱动器。<br /><br /> 将最终反斜杠包括在路径中。 | `Source\Repos\ConsoleApp1\ConsoleApp1\` |
| `MSBuildThisFileExtension` | 保留 | `MSBuildThisFileFullPath`的文件扩展名部分。 | `.csproj` |
| `MSBuildThisFileFullPath` | 保留 | 项目或包含正在运行目标的目标文件的绝对路径。<br /><br /> 提示:你可指定在相对于目标文件而不是相对于原始项目文件的目标文件中的相对路径。 | `c:\Source\Repos\ConsoleApp1\ConsoleApp1\ConsoleApp1.csproj` |
| `MSBuildThisFileName` | 保留 | `MSBuildThisFileFullPath` 的文件名部分，不包含文件扩展名。 | `ConsoleApp1` |
| `MSBuildToolsPath` | 保留 | 与 `MSBuildToolsVersion` 的值相关联的 MSBuild 版本的安装路径。<br /><br /> 不要将最终的反斜杠包含在路径中。<br /><br /> 不能重写此属性。 | `C:\Program Files (x86)\Microsoft Visual Studio\2019\Preview\MSBuild\Current\Bin` |
| `MSBuildToolsVersion` | 保留 | 用于生成项目的 MSBuild 工具集版本。<br /><br /> 注意：包含用于生成应用程序的任务、目标和工具的 MSBuild 工具集。 工具包括编译器，例如 csc.exe 和 vbc.exe 。 有关详细信息，请参阅[工具集 (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md) 和[标准和自定义工具集配置](../msbuild/standard-and-custom-toolset-configurations.md)。 | `Current` |
| `MSBuildVersion` | 保留 | 用于生成项目的 MSBuild 版本。 <br /><br/> 此属性不能重写，否则将返回 `MSB4004 - The 'MSBuildVersion' property is reserved, and can not be modified.` 错误消息。 | 16.7.0 |

## <a name="names-that-conflict-with-msbuild-elements"></a>与 MSBuild 元素冲突的名称

除上述名称外，对应于 MSBuild 语言元素的名称也不能用于用户定义的属性、项或项元数据：

* VisualStudioProject
* Target
* PropertyGroup
* Output
* ItemGroup
* UsingTask
* ProjectExtensions
* OnError
* ImportGroup
* Choose
* When
* Otherwise

## <a name="see-also"></a>请参阅

- [MSBuild 参考](../msbuild/msbuild-reference.md)

- [MSBuild 属性](../msbuild/msbuild-properties.md)
