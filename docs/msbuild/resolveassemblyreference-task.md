---
title: ResolveAssemblyReference 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ResolveAssemblyReference
- MSBuild.ResolveAssemblyReference.TurnOnAutoGenerateBindingRedirects
- MSBuild.ResolveAssemblyReference.FoundConflict
- MSBuild.ResolveAssemblyRedirects.SuggestedRedirects
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ResolveAssemblyReference task [MSBuild]
- MSBuild, ResolveAssemblyReference task
ms.assetid: 4d56d848-b29b-4dff-86a2-0a96c9e4a170
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 42fcd289f5258fde7ae8f17a9e19a25427fe6885
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2020
ms.locfileid: "77278354"
---
# <a name="resolveassemblyreference-task"></a>ResolveAssemblyReference 任务
确定依赖指定程序集的所有程序集，其中包括第二级和第 `n` 级的依赖项。

## <a name="parameters"></a>参数
 下表描述了 `ResolveAssemblyReference` 任务的参数。

|参数|描述|
|---------------|-----------------|
|`AllowedAssemblyExtensions`|可选 `String[]` 参数。<br /><br /> 将在解析引用时使用的程序集文件扩展名。 默认文件扩展名为 .exe 和 .dll。  |
|`AllowedRelatedFileExtensions`|可选 `String[]` 参数。<br /><br /> 要用于搜索彼此相互关联的文件的文件扩展名。 默认扩展名是 .pdb 和 .xml。  |
|`AppConfigFile`|可选 `String` 参数。<br /><br /> 指定从中进行分析和提取 bindingRedirect 映射的 app.config 文件。  如果指定此参数，则 `AutoUnify` 参数必须是 `false`。|
|`Assemblies`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定必须为其标识完整路径和依赖项的项。 这些项可以具有类似“System”的简单名称或类似“System, Version=2.0.3500.0, Culture=neutral, PublicKeyToken=b77a5c561934e089”的强名称。<br /><br /> 传递给此参数的项可选择性地包含以下项的元数据：<br /><br /> -   `Private`： `Boolean` 值。 如果为 `true`，则在本地复制该项。 默认值为 `true`。<br />-   `HintPath`： `String` 值。 指定要用作引用的路径和文件名。 当在 `SearchPaths` 参数内指定 {HintPathFromItem} 时使用此元数据。 默认值为一个空字符串。<br />-   `SpecificVersion`： `Boolean` 值。 如果为 `true`，则在 `Include` 特性内指定的确切名称必须匹配。 如果为 `false`，则具有同一简单名称的任何程序集都将起作用。 如果 `SpecificVersion` 未指定，则该任务会检查项中 `Include` 特性的值。 如果该特性是一个简单名称，则其行为方式如同 `SpecificVersion` 是 `false`。 如果该特性是一个强名称，则其行为方式如同 `SpecificVersion` 是 `true`。<br />     当与引用项类型搭配使用时， `Include` 特性必须是要解析的程序集的完整合成名称。 仅当合成名称完全匹配 `Include` 特性时才解析该程序集。<br />     如果项目面向 .NET Framework 版本，且引用了为更高版本 .NET Framework 编译的程序集，则该引用仅当 `SpecificVersion` 设置为 `true`。<br />     如果项目面向配置文件，且引用的程序集不位于该配置文件中，则该引用仅当 `SpecificVersion` 设置为 `true`。<br />-   `ExecutableExtension`： `String` 值。 当存在时，解析的程序集必须具有此扩展名。 当不存在时，对于每个检查的目录，最先考虑 .dll，其次考虑 .exe。  <br />-   `SubType`： `String` 值。 仅当项具有空的子类型元数据时才解析为完整的程序集路径。 具有非空子类型元数据的项将被忽略。<br />-   `AssemblyFolderKey`： `String` 值。 出于兼容目的支持此元数据。 它指定一个用户定义的注册表项，如“hklm\\\<VendorFolder>”，该 `Assemblies` 应用于解析程序集引用。 |
|`AssemblyFiles`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定为其查找依赖项的完全限定程序集列表。<br /><br /> 传递给此参数的项可选择性地包含以下项的元数据：<br /><br /> -   `Private`：可选 `Boolean` 值。 如果为 true，则在本地复制该项。<br />-   `FusionName`：可选的 `String` 元数据。 指定此项的简单名称或强名称。 若此特性存在，则可节省时间，因为不必打开程序集文件即可获取名称。|
|`AutoUnify`|可选 `Boolean` 参数。<br /><br /> 此参数用于构建程序集（如 DLL），它不能有一个普通的 App.Config 文件。 <br /><br /> 当为 `true` 时，会自动处理最后得到的依赖项关系图，如同向 AppConfigFile 参数传递了 App.Config 文件一样。  此虚拟 App.Config 文件对每组冲突程序集具有 bindingRedirect 条目，以便选择最高版本的程序集。  这样做的结果是避免有关冲突程序集的警告，因为每个冲突都将得到解决。<br /><br /> 当为 `true`时，每个不同的重映射将导致高优先级注释，显示新旧版本以及 `AutoUnify` 是 `true`。<br /><br /> 当为 `true` 时，AppConfigFile 参数必须为空。<br /><br /> 当为 `false`时，不会自动发生程序集版本重映射。 当存在两个版本的程序集时，将发出警告。<br /><br /> 当为 `false`时，同一个程序集不同版本间的不同冲突将导致高优先级注释。 这些注释后跟单个警告。 警告具有唯一的错误代码，其文本写有“找到不同引用版本和依赖程序集之间的冲突”。<br /><br /> 默认值为 `false`。|
|`CandidateAssemblyFiles`|可选 `String[]` 参数。<br /><br /> 指定用于搜索和解析过程的程序集列表。 传递给此参数的值必须是绝对文件名或项目相对文件名。<br /><br /> 当 `SearchPaths` 参数包含 {CandidateAssemblyFiles} 作为要考虑的路径之一时，将会考虑此列表中的程序集。|
|`CopyLocalDependenciesWhenParentReferenceInGac`|可选 <xref:System.Boolean> 参数。<br /><br /> 如果为 true，若要确定是否应在本地复制依赖项，则其中一项完成的检查是查看项目文件中的父引用是否设置了 Private 元数据。 如果设置了元数据，则将 Private 值用作依赖项。<br /><br /> 如果未设置元数据，则依赖项将进行与父引用相同的检查。 其中一项检查是查看该引用是否位于 GAC 中。 如果引用位于 GAC 中，则不会在本地复制它，因为假设它位于目标计算机上的 GAC 中。 这仅应用于特定的引用，而不是其依赖项。<br /><br /> 例如，位于 GAC 中的项目文件中的引用不在本地复制，但可在本地复制其依赖项，因为它们不在 GAC 中。<br /><br /> 如果为 false，则检查项目文件引用，以确定它们是否位于 GAC 中，并且视情况进行本地复制。<br /><br /> 检查依赖项以确定它们是否位于 GAC 中，还要确定项目文件的父引用是否位于 GAC 中。<br /><br /> 如果项目文件的父引用位于 GAC 中，则不在本地复制依赖项。<br /><br /> 无论此参数是为 true 还是 false，如果存在多个父引用，且任一父引用都不位于 GAC 中，则在本地复制所有这些父引用。|
|`CopyLocalFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 只读输出参数。<br /><br /> 返回 `ResolvedFiles`、 `ResolvedDependencyFiles`、 `RelatedFiles`、 `SatelliteFiles`和 `ScatterFiles` 参数中的每个具有值为 `CopyLocal` true `true`。|
|`FilesWritten`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含写入到磁盘的项。|
|`FindDependencies`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，将找到依赖项。 否则只找到主引用。 默认值为 `true`。|
|`FindRelatedFiles`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则将找到相关文件，如 .pdb 文件和 xml 文件。   默认值为 `true`。|
|`FindSatellites`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则将找到附属程序集。 默认值为 `true.`|
|`FindSerializationAssemblies`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则该任务搜索序列化程序集。 默认值为 `true`。|
|`FullFrameworkAssemblyTables`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定包含“FrameworkDirectory”元数据的项以关联 redist 列表与特定的框架目录。 如不进行关联，则将记录错误。 如未设置 FrameworkDirectory，则解析程序集引用 (RAR) 逻辑将使用目标框架目录。|
|`FullFrameworkFolders`|可选 <xref:System.String?displayProperty=fullName>`[]` 参数。<br /><br /> 指定包含 RedistList 目录的文件夹。 此目录表示给定客户端配置文件的完整框架，例如 %programfiles%\reference assemblies\microsoft\framework\v4.0。 |
|`FullTargetFrameworkSubsetNames`|可选 `String[]` 参数。<br /><br /> 包含目标框架子集名称的列表。 如果列表中的子集名称匹配 `TargetFrameworkSubset` 名称属性中的一个名称，则系统将排除生成时的特定目标框架子集。|
|`IgnoreDefaultInstalledAssemblyTables`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则该任务搜索并使用位于 `TargetFrameworkDirectories` 下 \RedistList 目录中的其他已安装程序集表（或“Redist 列表”）。  默认值为 `false.`|
|`IgnoreDefaultInstalledAssemblySubsetTables`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则该任务搜索并使用位于 `TargetFrameworkDirectories` 下 \SubsetList 目录中的其他已安装程序集子集表（或“子集列表”）。  默认值为 `false.`|
|`InstalledAssemblySubsetTables`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 包含 XML 文件的列表，该文件指定应位于目标子集中的程序集。<br /><br /> 根据需要，此列表中的项可指定“FrameworkDirectory”元数据以关联 `InstalledAssemblySubsetTable`<br /><br /> 与特定的框架目录。<br /><br /> 如果只有一个 `TargetFrameworkDirectories` 元素，则对于此列表中缺少“FrameworkDirectory”元数据的任何项，我们将其视为好像它们被设置为传递到 `TargetFrameworkDirectories`的唯一值。|
|`InstalledAssemblyTables`|可选 `String` 参数。<br /><br /> 包含 XML 文件的列表，该文件指定应安装到目标计算机上的程序集。<br /><br /> 当设置了 `InstalledAssemblyTables` 时，列表中早期版本的程序集将合并到 XML 中所列的较新版本。 此外，具有 InGAC='true' 设置的程序集被视为先决条件，且将设置为 CopyLocal='false'（除非显式重写）。<br /><br /> 根据需要，此列表中的项可指定“FrameworkDirectory”元数据以关联 `InstalledAssemblyTable` 与特定的框架目录。  但将忽略此设置，除非 Redist 名称以<br /><br /> “Microsoft-Windows-CLRCoreComp”开头。<br /><br /> 如果只有一个 `TargetFrameworkDirectories` 元素，则对于此列表中缺少“FrameworkDirectory”元数据的任何项，我们将其视为好像它们被设置为传递到<br /><br /> `TargetFrameworkDirectories`的唯一值。|
|`LatestTargetFrameworkDirectories`|可选 `String[]` 参数。<br /><br /> 指定目录列表，其中包含该计算机上可将其作为目标的最新框架的 redist 列表。 如果未设置此项，则使用安装在给定目标框架标识符的计算机上的最高框架。|
|`ProfileName`|可选 `String` 参数。<br /><br /> -   指定要设定为目标的框架配置文件的名称。 例如，客户端、Web 或网络。|
|`RelatedFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 只读输出参数。<br /><br /> 包含与引用具有相同基名称的相关文件，如 XML 和 .pdb 文件。 <br /><br /> 此参数中列出的文件可选择性地包含以下项的元数据：<br /><br /> -   `Primary`： `Boolean` 值。 如果为 `true`，则文件项已通过使用 `Assemblies` 参数。 默认值是 `false`。<br />-   `CopyLocal`： `Boolean` 值。 指示给定引用是否应复制到输出目录。|
|`ResolvedDependencyFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 只读输出参数。<br /><br /> 包含第 *n*级依赖项路径。 此参数不包括第一级主引用，其包含在 `ResolvedFiles` 参数中。<br /><br /> 此参数中的项选择性地包含以下项的元数据：<br /><br /> -   `CopyLocal`： `Boolean` 值。 指示给定引用是否应复制到输出目录。<br />-   `FusionName`： `String` 值。 指定此依赖项的名称。<br />-   `ResolvedFrom`： `String` 值。 指定已从中解析此文件的文字搜索路径。|
|`ResolvedFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 只读输出参数。<br /><br /> 包含已解析为完整路径的所有主引用列表。<br /><br /> 此参数中的项选择性地包含以下项的元数据：<br /><br /> -   `CopyLocal`： `Boolean` 值。 指示给定引用是否应复制到输出目录。<br />-   `FusionName`： `String` 值。 指定此依赖项的名称。<br />-   `ResolvedFrom`： `String` 值。 指定已从中解析此文件的文字搜索路径。|
|`SatelliteFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 只读输出参数。<br /><br /> 指定找到的任何附属文件。 如果导致此项存在的引用或依赖项是 CopyLocal=true，则这些将为 CopyLocal=true。<br /><br /> 此参数中的项选择性地包含以下项的元数据：<br /><br /> -   `CopyLocal`： `Boolean` 值。 指示给定引用是否应复制到输出目录。 如果导致此项存在的引用或依赖项具有为 `true` 的 `CopyLocal` 值，则这个值为 `true`。<br />-   `DestinationSubDirectory`： `String` 值。 指定要复制此项到的相对目标目录。|
|`ScatterFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 只读输出参数。<br /><br /> 包含与某个给定的程序集关联的散点文件。<br /><br /> 此参数中的项选择性地包含以下项的元数据：<br /><br /> -   `CopyLocal`： `Boolean` 值。 指示给定引用是否应复制到输出目录。|
|`SearchPaths`|必选 `String[]` 参数。<br /><br /> 指定目录或特殊位置，将在其中进行搜索以找到磁盘上表示程序集的文件。 列出搜索路径的顺序非常重要。 对于每个程序集，从左到右搜索路径的列表。 当找到表示该程序集的文件时，该搜索即停止，并且开始搜索下一个程序集。<br /><br /> 此参数接受以分号分隔的值列表，这些值可以是目录路径，也可以是下表中的特殊文本值：<br /><br /> -   `{HintPathFromItem}`：指定任务将检查基项的 `HintPath` 元数据。<br />-   `{CandidateAssemblyFiles}`：指定任务将检查通过 `CandidateAssemblyFiles` 参数传入的文件。<br />-   `{Registry:` \<AssemblyFoldersBase>、\<RuntimeVersion>、\<AssemblyFoldersSuffix>`}`：指定任务将在注册表中指定的其他文件夹中进行搜索。 \<AssemblyFoldersBase>、\<RuntimeVersion> 和 \<AssemblyFoldersSuffix> 应替换为要搜索的注册表位置的特定值。 常见目标中的默认规范是 {Registry:$(FrameworkRegistryBase)、$(TargetFrameworkVersion)、$(AssemblyFoldersSuffix)、$(AssemblyFoldersExConditions)}。<br />-   `{AssemblyFolders}`：指定任务将使用 Visual Studio.NET 2003 finding-assemblies-from-registry（从注册表查找程序集）方案。<br />-   `{GAC}`：指定任务将在全局程序集缓存 (GAC) 中搜索。<br />-   `{RawFileName}`：指定任务将项的 `Include` 值视为确切的路径和文件名。|
|`SerializationAssemblyFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 只读输出参数。<br /><br /> 包含找到的任何 XML 序列化程序集。 如果导致此项存在的引用或依赖项是 CopyLocal=true，则这些项被标记为 CopyLocal=true。<br /><br /> `Boolean` 元数据 CopyLocal 指示给定的引用是否应该复制到输出目录。|
|`Silent`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则不记录任何信息。 默认值为 `false`。|
|`StateFile`|可选 `String` 参数。<br /><br /> 指定一个文件名，该文件名表示用于保存此任务的中间生成状态的位置。|
|`SuggestedRedirects`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 只读输出参数。<br /><br /> 针对每个不同的冲突程序集标识包含一个项，而不考虑 `AutoUnify` 参数的值。 这包括发现在应用程序配置文件中没有合适的 bindingRedirect 条目的每个区域性 和 PKT。<br /><br /> 每个项选择性地包含以下信息：<br /><br /> -   `Include` 属性：包含版本字段值为 0.0.0.0 的程序集系列的完整名称<br />-   `MaxVersion` 项元数据：包含的最大版本号。|
|`TargetedRuntimeVersion`|可选 `String` 参数。<br /><br /> 指定设为目标的运行时版本，例如，2.0.57027 或 v2.0.57027。|
|`TargetFrameworkDirectories`|可选 `String[]` 参数。<br /><br /> 指定目标框架目录的路径。 需要此参数来确定生成的项的 CopyLocal 状态。<br /><br /> 如果未指定此参数，则没有生成的项将具有为 `true` 的 CopyLocal 值，除非在其源项上显式具有为 `true` 的 `Private` 元数据值。|
|`TargetFrameworkMoniker`|可选 `String` 参数。<br /><br /> 要监视的 TargetFrameworkMoniker（如果有）。 这用于日志记录。|
|`TargetFrameworkMonikerDisplayName`|可选 `String` 参数。<br /><br /> 要监视的 TargetFrameworkMoniker 显示名称（如果有）。 这用于日志记录。|
|`TargetFrameworkSubsets`|可选 `String[]` 参数。<br /><br /> 包含要在目标框架目录中搜索的目标框架子集名称的列表。|
|`TargetFrameworkVersion`|可选 `String` 参数。<br /><br /> 项目目标框架版本。 默认值为空，意味着没有用于基于目标框架的引用的筛选。|
|`TargetProcessorArchitecture`|可选 `String` 参数。<br /><br /> 首选的目标处理器架构。 用于解析全局程序集缓存 (GAC) 引用。<br /><br /> 此参数可以具有 `x86`、`IA64` 或 `AMD64` 的值。<br /><br /> 如果缺少此参数，则该任务首先考虑与当前正在运行的进程架构匹配的程序集。 如果未找到程序集，该任务将考虑位于 GAC 中 `ProcessorArchitecture` 值为 `MSIL` 或没有 `ProcessorArchitecture` 值的程序集。|

## <a name="warnings"></a>警告
 将记录以下警告：

- `ResolveAssemblyReference.TurnOnAutoGenerateBindingRedirects`

- `ResolveAssemblyReference.SuggestedRedirects`

- `ResolveAssemblyReference.FoundConflicts`

- `ResolveAssemblyReference.AssemblyFoldersExSearchLocations`

- `ResolveAssemblyReference.UnifiedPrimaryReference`

- `ResolveAssemblyReference.PrimaryReference`

- `ResolveAssemblyReference.UnifiedDependency`

- `ResolveAssemblyReference.UnificationByAutoUnify`

- `ResolveAssemblyReference.UnificationByAppConfig`

- `ResolveAssemblyReference.UnificationByFrameworkRetarget`

## <a name="remarks"></a>备注
 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="see-also"></a>请参阅
- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
