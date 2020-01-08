---
title: Visual Studio 集成 (MSBuild)
titleSuffix: ''
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, reference resolution
- MSBuild, well-known target names
- MSBuild, hosting
- MSBuild, editing project files
- MSBuild, Visual Studio integration
- MSBuild, IntelliSense
- MSBuild, output groups
- MSBuild, in-process compilers
- MSBuild, design-time target execution
ms.assetid: 06cd6d7f-8dc1-4e49-8a72-cc9e331d7bca
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b1ddb8bdbc913a72791144d5e9d29d206712a3d6
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594417"
---
# <a name="visual-studio-integration-msbuild"></a>Visual Studio 集成 (MSBuild)
Visual Studio 承载有 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]，用以加载和生成托管项目。 由于 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 负责处理项目，因此，可以在 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 中成功使用几乎任何 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 格式的项目（即使项目是用另一种工具编写的，而且这些项目有自定义的生成过程）。

 自定义希望在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中加载和生成的项目和 .targets  文件时，应当考虑 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 的 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]承载的特定方面，本文对此进行了描述。 这些内容将帮助你确保 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中诸如 IntelliSense 和调试这样的功能对你的自定义项目有效。

 有关 C++ 项目的信息，请参阅 [Project Files](/cpp/build/reference/project-files)。

## <a name="project-file-name-extensions"></a>项目文件扩展名
 MSBuild.exe  可识别与 .\*proj  模式匹配的任何项目文件扩展名。 但是，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 只识别其中一部分项目文件扩展名，这些扩展名决定了将会加载项目的特定于语言的项目系统。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 没有基于非特定语言 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 的项目系统。

 例如，[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 项目系统可加载 .csproj  文件，但是 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 不能加载 .xxproj  文件。 任意语言的源文件对应的项目文件都必须使用与 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 或 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 项目文件相同的扩展名，才能加载到 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中。

## <a name="well-known-target-names"></a>已知的目标名称
 单击 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中的“生成”  命令会执行项目中的默认目标。 通常，此目标也命名为 `Build`。 如果选择 **“重新生成”** 或 **“清理”** 命令，将尝试执行项目中的同名目标。 单击 **“发布”** 将执行项目中的名为 `PublishOnly` 的目标。

## <a name="configurations-and-platforms"></a>配置和平台
 在 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 项目中，配置由在包含 `PropertyGroup` 特性的 `Condition` 元素中进行分组的属性来表示。 为了创建要显示的项目配置和平台的列表，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 将检查这些条件。 若要成功提取此列表，条件必须具有如下格式：

```xml
Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' "
Condition=" '$(Configuration)' == 'Release' " 
Condition=" '$(Something)|$(Configuration)|$(SomethingElse)' == 'xxx|Debug|yyy' "
```

 为了达到这个目的，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 将针对 `PropertyGroup`, `ItemGroup`, `Import`、属性和项元素检查条件。

## <a name="additional-build-actions"></a>其他生成操作
 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 可用于通过“文件”属性  窗口的“生成操作”  属性更改项目中文件的项类型名称。 Compile  、EmbeddedResource  、Content  和 None  项类型名称始终会在此菜单中列出，此菜单中同时还会列出项目中已有的任何其他项类型名称。 若要确保任何自定义的项类型名称在此菜单中始终可用，可以将这些名称添加到名为 `AvailableItemName`的项类型。 例如，如果在项目文件中添加下面的内容，就会为导入它的所有项目在此菜单中添加自定义类型 JScript  ：

```xml
<ItemGroup>
    <AvailableItemName Include="JScript"/>
</ItemGroup>
```

> [!NOTE]
> 某些项类型名称是 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 所特有的，但没有在此下拉列表中列出。

## <a name="in-process-compilers"></a>进程内编译器
 如果可能， [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 将尝试使用进程内版本的 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 编译器来提高性能。 （不适用于 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]。）为了让它正确工作，必须满足下面的条件：

- 在项目的目标中，必须具有名为 `Vbc` 的任务（适用于 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 项目）。

- 任务的 `UseHostCompilerIfAvailable` 参数必须设置为 True。

## <a name="design-time-intellisense"></a>设计时 IntelliSense
 在生成过程生成输出程序集之前，若要在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中获得 IntelliSense 支持，必须满足下面的条件：

- 必须有名为 `Compile`的目标。

- `Compile` 目标或它的一个依赖项必须调用该项目的编译器任务，例如， `Csc` 或 `Vbc`。

- `Compile` 目标或它的一个依赖项必须导致编译器接收使用 IntelliSense 所需的所有参数，特别是所有引用。

- [进程内编译器](#in-process-compilers)部分中列出的条件必须满足。

## <a name="build-solutions"></a>生成解决方案
 在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中，解决方案文件和项目生成顺序由 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 本身进行控制。 在命令行用 msbuild.exe  生成解决方案时，[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 将分析解决方案文件，并对项目生成进行排序。 在这两种情况下，项目都将按依赖顺序逐个生成，因此，不会来回进行项目到项目的引用。 相比之下，用 msbuild.exe  生成单个项目时，则会来回进行项目到项目的引用。

 在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 内生成时，属性 `$(BuildingInsideVisualStudio)` 将设置为 `true`。 这可以用在项目或 .targets  文件中，使生成行为有所不同。

## <a name="display-properties-and-items"></a>显示属性和项
 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 可识别某些属性名称和值。 例如，项目中下面的属性将导致 **“Windows 应用程序”** 出现在 **“项目设计器”** 内的 **“应用程序类型”** 框中。

```xml
<OutputType>WinExe</OutputType>
```

 可以在 **“项目设计器”** 中编辑属性值，并将其保存在项目文件中。 如果通过手动编辑来为这样的属性分配了无效的值，则 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 在加载项目时会显示一条警告，并会用默认值替代无效值。

 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 知道某些属性的默认值。 这些属性不会保留到项目文件中，除非它们有非默认的值。

 具有任意名称的属性不会显示在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中。 若要在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中修改任意属性，必须在 XML 编辑器中打开项目文件，并手动编辑它们。 有关详细信息，请参阅本主题后面的[在 Visual Studio 中编辑项目文件](#edit-project-files-in-visual-studio)一节。

 默认情况下，在项目中定义的具有任意项类型名称的项将会显示在解决方案资源管理器  中其项目节点的下面。 若要隐藏项，请将 `Visible` 元数据设置为 `false`。 例如，下面的项将参与生成过程，但不会显示在解决方案资源管理器  中。

```xml
<ItemGroup>
    <IntermediateFile Include="cache.temp">
        <Visible>false</Visible>
    </IntermediateFile>
</ItemGroup>
```

 默认情况下，不会显示在导入到项目内的文件中所声明的项。 在生成过程中创建的项永远不会显示在解决方案资源管理器  中。

## <a name="conditions-on-items-and-properties"></a>项和属性的条件
 在生成期间，将严格检查所有条件。

 在确定要显示的属性值时，会以不同的方式来计算 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 认为依赖于配置的属性和它认为独立于配置的属性。 对于它认为依赖于配置的属性，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 将相应地设置 `Configuration` 和 `Platform` 属性，并指示 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 重新计算项目。 对于它认为独立于配置的属性，计算条件的方式则是不确定的。

 如果项的条件表达式用于决定是否应当在解决方案资源管理器  中显示项，则始终忽略这样的表达式。

## <a name="debugging"></a>调试
 为了查找和启动输出程序集并附加调试器，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 需要正确定义属性 `OutputPath`、`AssemblyName` 和 `OutputType`。 如果生成过程没有导致编译器生成 .pdb  文件，则调试器将无法附加。

## <a name="design-time-target-execution"></a>设计时目标执行
 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 加载项目时，它将尝试执行具有某些名称的目标。 这些目标包括 `Compile`、`ResolveAssemblyReferences`、`ResolveCOMReferences`、`GetFrameworkPaths` 和 `CopyRunEnvironmentFiles`。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 将运行这些目标，以便可以执行以下操作：初始化编译器以提供 IntelliSense，初始化调试器，以及解析在解决方案资源管理器中显示的引用。 如果这些目标不出现，项目将正确加载和生成，但是 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中的设计时体验将不会完全有效。

## <a name="edit-project-files-in-visual-studio"></a>在 Visual Studio 中编辑项目文件
 若要直接编辑 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 项目，你可以在 Visual Studio XML 编辑器中打开项目文件。

#### <a name="to-unload-and-edit-a-project-file-in-visual-studio"></a>在 Visual Studio 中卸载和编辑项目文件

1. 在 **“解决方案资源管理器”** 中，打开项目的快捷菜单，然后选择 **“卸载项目”** 。

     该项目即被标记为 **“(不可用)”** 。

2. 在“解决方案资源管理器”  中，打开不可用项目的快捷菜单，然后选择“编辑 \<项目文件>”  。

     该项目文件即在 Visual Studio XML 编辑器中打开。

3. 编辑、保存，然后关闭项目文件。

4. 在 **“解决方案资源管理器”** 中，打开不可用项目的快捷菜单，然后选择 **“重新加载项目”** 。

## <a name="intellisense-and-validation"></a>IntelliSense 和验证
 使用 XML 编辑器编辑项目文件时，IntelliSense 和验证由 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 架构文件驱动。 这些安装在架构缓存中，安装目录为 \<Visual Studio 安装目录>\Xml\Schemas\1033\MSBuild  。

 核心 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 类型是在 Microsoft.Build.Core.xsd  中定义的，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 使用的通用类型则是在 Microsoft.Build.CommonTypes.xsd  中定义的。 若要自定义架构，以便设置针对自定义项类型名称、属性和任务的 IntelliSense 和验证，可以编辑 Microsoft.Build.xsd  ，或创建包括 CommonTypes 或核心架构的自己的架构。 如果创建自己的架构，则必须使用 **“属性”** 窗口指引 XML 编辑器找到它。

## <a name="edit-loaded-project-files"></a>编辑加载的项目文件
 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 将缓存项目文件和由项目文件导入的文件的内容。 如果编辑已加载的项目文件，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 将自动提示你重新加载项目，以使更改生效。 但是，如果编辑由已加载的项目导入的文件，则没有重新加载的提示，并且你必须手动卸载并重新加载项目，以使更改生效。

## <a name="output-groups"></a>输出组
 Microsoft.Common.targets  中定义的一些目标的名称以 `OutputGroups` 或 `OutputGroupDependencies` 结尾。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 调用这些目标以获取项目输出的特定列表。 例如，`SatelliteDllsProjectOutputGroup` 目标创建将由一次生成过程创建的所有附属程序集的列表。 诸如发布、部署和项目到项目引用这样的功能将使用这些输出组。 没有定义它们的项目仍然可以在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中加载和生成，但是某些功能可能无法正常工作。

## <a name="reference-resolution"></a>引用解析
 引用解析是使用项目文件中存储的引用项来查找实际程序集的过程。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 必须触发引用解析，才能在 **“属性”** 窗口中显示每个引用的详细属性。 下面的列表描述了三种类型引用和如何解析它们。

- 程序集引用：

   项目系统调用具有已知名称 `ResolveAssemblyReferences`的目标。 此目标应当产生具有项类型名称 `ReferencePath`的项。 这些项中的每一个都应当有包含引用的完整路径的项规范（项的 `Include` 特性的值）。 除了下面的新元数据以外，项应当让来自输入项的所有元数据通过：

  - `CopyLocal`，指示程序集是否应当复制到输出文件夹中、设置为 True 还是 False。

  - `OriginalItemSpec`，包含引用的原始项规范。

  - `ResolvedFrom`，如果从 .NET Framework 目录解析它，则设置为“{TargetFrameworkDirectory}”。

- COM 引用：

   项目系统调用具有已知名称 `ResolveCOMReferences`的目标。 此目标应当产生具有项类型名称 `ComReferenceWrappers`的项。 这些项中的每一个都应当有项规范，其中包含 COM 引用的 interop 程序集的完整路径。 除了具有名称 `CopyLocal`（用于指示程序集是否应当复制到输出文件夹中、设置为 true 还是 false）的新元数据以外，项应当让来自输入项的所有元数据通过。

- 本机引用

   项目系统调用具有已知名称 `ResolveNativeReferences`的目标。 此目标应当产生具有项类型名称 `NativeReferenceFile`的项。 除了名为 `OriginalItemSpec`（包含引用的原始项规范）的新元数据片段以外，项应当让来自输入项的所有元数据通过。

## <a name="performance-shortcuts"></a>性能快捷方式
 如果使用 Visual Studio IDE 开始调试（通过选择 F5 或选择菜单栏中的“调试”   > “启动调试”  ）或生成项目（例如，通过选择“生成”   > “生成解决方案”  ），则生成过程将使用快速更新检查来提高性能。 在有些情况下，当自定义的生成创建轮流生成的文件时，快速更新检查无法正确标识更改的文件。 通过设置环境变量 `DISABLEFASTUPTODATECHECK=1`，需要更彻底更新检查的项目可以关闭快速检查。 或者，项目可在项目或项目导入的文件中将此变量设置为 MSBuild 属性。

 对于 Visual Studio 中的常规生成，将不适用快速更新检查，项目的生成就像在命令提示符处调用生成一样。

## <a name="see-also"></a>请参阅
- [如何：扩展 Visual Studio 生成过程](../msbuild/how-to-extend-the-visual-studio-build-process.md)
- [在 IDE 中启动生成](../msbuild/starting-a-build-from-within-the-ide.md)
- [注册 .NET Framework 的扩展](../msbuild/registering-extensions-of-the-dotnet-framework.md)
- [MSBuild 概念](../msbuild/msbuild-concepts.md)
- [Item 元素 (MSBuild)](../msbuild/item-element-msbuild.md)
- [Property 元素 (MSBuild)](../msbuild/property-element-msbuild.md)
- [Target 元素 (MSBuild)](../msbuild/target-element-msbuild.md)
- [Csc 任务](../msbuild/csc-task.md)
- [Vbc 任务](../msbuild/vbc-task.md)
