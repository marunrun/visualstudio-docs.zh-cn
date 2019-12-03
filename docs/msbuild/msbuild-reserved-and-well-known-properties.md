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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9bd54e97535c281d50119fdc7aa759d0704fa9e1
ms.sourcegitcommit: b5cb0eb09369677514ee1f44d5d7050d34c7fbc1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2019
ms.locfileid: "74491557"
---
# <a name="msbuild-reserved-and-well-known-properties"></a>MSBuild 保留属性和已知属性
[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 提供了一组预定义的属性，这些属性存储有关项目文件和 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 二进制文件的信息。 这些属性的计算方式与其他 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 属性相同。 例如，要使用 `MSBuildProjectFile` 属性，应键入 `$(MSBuildProjectFile)`。

 MSBuild 使用下表中的值预定义保留的属性和已知的属性。 无法重写保留的属性，但可以使用名称相同的环境属性、全局属性或已在项目文件中声明的属性重写已知的属性。

## <a name="reserved-and-well-known-properties"></a>保留属性和已知属性
 下表介绍了 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 预定义的属性。

| 属性 | 保留或已知 | 说明 |
|----------------------------------|------------------------| - |
| `MSBuildBinPath` | 保留 | 当前正在使用的 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 二进制文件所在文件夹的绝对路径（例如，C:\Windows\Microsoft.Net\Framework\\\<versionNumber>  ）。 如果你必须引用 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 目录中的文件，此属性将非常有用。<br /><br /> 不要在此属性上添加最终反斜杠。 |
| `MSBuildExtensionsPath` | 已知 | 在 .NET Framework 4 中引入：`MSBuildExtensionsPath` 和 `MSBuildExtensionsPath32` 的默认值之间没有差异。 你可以设置环境变量 `MSBUILDLEGACYEXTENSIONSPATH` 为非 null 值，以启用早期版本中的 `MSBuildExtensionsPath`的默认值的行为。<br /><br /> 在 .NET Framework 3.5 和较早的版本中，根据当前进程的位数，`MSBuildExtensionsPath` 的默认值指向位于 \Program Files\\ 或 \Program Files (x86) 文件夹下的 MSBuild 子文件夹路径   。 例如，对于在 64 位计算机上的 32 位进程，此属性指向 \Program Files (x86) 文件夹  。 对于在 64 位计算机上的 64 位进程，此属性指向 \Program Files 文件夹  。<br /><br /> 不要在此属性上添加最终反斜杠。<br /><br /> 此位置用于存放自定义目标文件。 例如，目标文件可能安装在 \Program Files\MSBuild\MyFiles\Northwind.targets 中，然后使用此 XML 代码导入到项目文件中  ：<br /><br /> `<Import Project="$(MSBuildExtensionsPath)\MyFiles\Northwind.targets"/>` |
| `MSBuildExtensionsPath32` | 已知 | 位于 \Program Files 或 \Program Files (x86) 文件夹下的 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 子文件夹的路径   。 此路径始终指向 32 位计算机上的 32 位 \Program Files (x86) 文件夹和 64 位计算机上的 \Program Files   。 另请参见 `MSBuildExtensionsPath` 和 `MSBuildExtensionsPath64`。<br /><br /> 不要在此属性上添加最终反斜杠。 |
| `MSBuildExtensionsPath64` | 已知 | 位于 \Program Files 文件夹下的 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 子文件夹的路径  。 对于 64 位计算机，此路径始终指向 \Program Files 文件夹  。 对于 32 位计算机，此路径为空。 另请参见 `MSBuildExtensionsPath` 和 `MSBuildExtensionsPath32`。<br /><br /> 不要在此属性上添加最终反斜杠。 |
| `MSBuildLastTaskResult` | 保留 | `true`，如果前一项任务完成没有出现任何错误（即使有警告）；否则如果前一项任务出现错误，则为 `false`。 通常，当任务中出现错误时，错误会发生在项目的最后。 因此，此属性的值决不会是 `false`，但以下情况除外：<br /><br /> - [Task 元素 (MSBuild)](../msbuild/task-element-msbuild.md) 的 `ContinueOnError` 属性设置为 `WarnAndContinue`（或 `true`）或 `ErrorAndContinue` 时。<br /><br /> - `Target` 将 [OnError 元素 (MSBuild)](../msbuild/onerror-element-msbuild.md) 作为子元素时。 |
| `MSBuildNodeCount` | 保留 | 生成过程中使用的并发进程的最大数目。 这是在命令行中为 -maxcpucount  指定的值。 如果指定了 -maxcpucount  但没有指定值，`MSBuildNodeCount` 会指定计算机中的处理器数。 有关详细信息，请参阅[命令行参考](../msbuild/msbuild-command-line-reference.md)和[并行生成多个项目](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)。 |
| `MSBuildProgramFiles32` | 保留 | 32 位程序文件夹的位置；例如，C:\Program Files (x86)  。<br /><br /> 不要在此属性上添加最终反斜杠。 |
| `MSBuildProjectDefaultTargets` | 保留 | `DefaultTargets` 元素的 `Project` 特性中指定的目标的完整列表。 例如，下面的 `Project` 元素的 `MSBuildDefaultTargets` 属性值为 `A;B;C`：<br /><br /> `<Project DefaultTargets="A;B;C" >` |
| `MSBuildProjectDirectory` | 保留 | 项目文件所在目录的绝对路径，例如，C:\MyCompany\MyProduct  。<br /><br /> 不要在此属性上添加最终反斜杠。 |
| `MSBuildProjectDirectoryNoRoot` | 保留 | `MSBuildProjectDirectory` 属性的值，但不包括根驱动器。<br /><br /> 不要在此属性上添加最终反斜杠。 |
| `MSBuildProjectExtension` | 保留 | 项目文件的文件扩展名（包括点号）；例如，.proj  。 |
| `MSBuildProjectFile` | 保留 | 项目文件的完整文件名（包括文件扩展名）；例如，MyApp.proj  。 |
| `MSBuildProjectFullPath` | 保留 | 项目文件的绝对路径和完整文件名（包括文件扩展名）；例如，C:\MyCompany\MyProduct\MyApp.proj  。 |
| `MSBuildProjectName` | 保留 | 项目文件的文件名（不包括文件扩展名）；例如，MyApp  。 |
| `MSBuildRuntimeType` | 保留 | 当前正在执行的运行时类型。 在 MSBuild 15 中引入。 可能未定义值（MSBuild 15 之前），`Full` 指示 MSBuild 在桌面 .NET Framework 上运行，`Core` 指示 MSBuild 在 .NET Core 上运行（例如在 `dotnet build` 中），`Mono` 指示 MSBuild 在 Mono 上运行。 |
| `MSBuildStartupDirectory` | 保留 | 在其中调用 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 的文件夹的绝对路径。 通过使用此属性，你无需在每个目录中都创建 \<dirs>.proj 文件就可以在项目树中的某个特定点下生成所有内容  。 而你只有一个项目，例如 c:\traversal.proj（如此处所示）  ：<br /><br /> `<Project ...>     <ItemGroup>         <ProjectFiles              Include="$            (MSBuildStartupDirectory)            **\*.csproj"/>     </ItemGroup>     <Target Name="build">         <MSBuild             Projects="@(ProjectFiles)"/>     </Target> </Project>`<br /><br /> 若要在该树中的任意一点生成，请键入：<br /><br /> `msbuild c:\traversal.proj`<br /><br /> 不要在此属性上添加最终反斜杠。 |
| `MSBuildThisFile` | 保留 | `MSBuildThisFileFullPath` 的文件名和文件扩展名部分。 |
| `MSBuildThisFileDirectory` | 保留 | `MSBuildThisFileFullPath` 的目录部分。<br /><br /> 将最终反斜杠包括在路径中。 |
| `MSBuildThisFileDirectoryNoRoot` | 保留 | `MSBuildThisFileFullPath` 的目录部分不包括根驱动器。<br /><br /> 将最终反斜杠包括在路径中。 |
| `MSBuildThisFileExtension` | 保留 | `MSBuildThisFileFullPath`的文件扩展名部分。 |
| `MSBuildThisFileFullPath` | 保留 | 项目或包含正在运行目标的目标文件的绝对路径。<br /><br /> 提示:你可指定在相对于目标文件而不是相对于原始项目文件的目标文件中的相对路径。 |
| `MSBuildThisFileName` | 保留 | `MSBuildThisFileFullPath` 的文件名部分，不包含文件扩展名。 |
| `MSBuildToolsPath` | 保留 | 与 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]的值相关联的 `MSBuildToolsVersion` 版本的安装路径。<br /><br /> 不要将最终的反斜杠包含在路径中。<br /><br /> 不能重写此属性。 |
| `MSBuildToolsVersion` | 保留 | 用于生成项目的 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 工具集版本。<br /><br /> 注意：包含用于生成应用程序的任务、目标和工具的 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 工具集。 工具包括编译器，例如 csc.exe 和 vbc.exe   。 有关详细信息，请参阅[工具集 (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md) 和[标准和自定义工具集配置](../msbuild/standard-and-custom-toolset-configurations.md)。 |
| `MSBuildVersion` | 保留 | 用于生成项目的 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 版本。 <br /><br/> 此属性不能重写，否则将返回 `MSB4004 - The 'MSBuildVersion' property is reserved, and can not be modified.` 错误消息。 |

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
