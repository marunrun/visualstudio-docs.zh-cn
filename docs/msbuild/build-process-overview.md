---
title: MSBuild 如何生成项目
ms.date: 05/18/2020
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, build process overview
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c3c1cdc4738f60301435932b3700f14377f12172
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290822"
---
# <a name="how-msbuild-builds-projects"></a>MSBuild 如何生成项目

MSBuild 的实际工作原理是什么？ 在本文中，你将了解 MSBuild 如何处理项目文件，无论是从 Visual Studio 调用，还是从命令行或脚本调用。 了解 MSBuild 的工作方式可以帮助你更好地诊断问题并更好地自定义生成过程。 本文介绍了生成过程，该过程在很大程度上适用于所有项目类型。

完整的生成过程包括生成项目的目标和任务的[初始启动](#startup)、[评估](#evaluation-phase)和[执行](#execution-phase)。 除了这些输入以外，外部导入还会定义生成过程的详细信息，包括[标准导入](#standard-imports)，如解决方案或项目级别的 Microsoft.Common.targets 和 [user-configurable imports](#user-configurable-imports)。

## <a name="startup"></a>启动

可通过 Microsoft.Build.dll 中的 MSBuild 对象模型，或者在命令行上或在脚本（如 CI 系统中）中直接调用可执行文件，从 Visual Studio 调用 MSBuild。 在任一情况下，影响生成过程的输入都包括项目文件（或 Visual Studio 内部的项目对象），可能是解决方案文件、环境变量、命令行开关或其对象模型等效项。 在启动阶段，使用命令行选项或对象模型等效项来配置 MSBuild 设置，如配置记录器。 使用 `-property` 或 `-p` 开关在命令行上设置的属性设置为全局属性，这些属性将重写项目文件中设置的任何值，即使稍后读取项目文件也是如此。

以下各节介绍了输入文件，如解决方案文件或项目文件。

### <a name="solutions-and-projects"></a>解决方案和项目

作为解决方案的一部分，MSBuild 实例可能包含一个项目，也可以包含多个项目。 解决方案文件不是 MSBuild XML 文件，但 MSBuild 会将其解释为了解需要针对给定的配置和平台设置生成的所有项目。 当 MSBuild 处理此 XML 输入时，称为解决方案生成。 它有一些可扩展点，使你能够在每个解决方案生成中运行一些内容，但由于此生成是独立于单个项目生成单独运行的，因此，解决方案生成中的属性或目标定义的设置与每个项目生成均不相关。

可在[自定义解决方案生成](customize-your-build.md#customize-the-solution-build)中了解如何扩展解决方案生成。

### <a name="visual-studio-builds-vs-msbuildexe-builds"></a>Visual Studio 生成与MSBuild.exe 生成

在 Visual Studio 中生成项目与通过 MSBuild 可执行文件直接调用 MSBuild 或使用 MSBuild 对象模型启动生成之间，有一些显著的区别。 Visual Studio 管理 Visual Studio 生成的项目生成顺序；它仅在单个项目级别调用 MSBuild，并在执行此操作时，将设置几个布尔属性（`BuildingInsideVisualStudio`、`BuildProjectReferences`），这对 MSBuild 的功能有很大影响。 在每个项目中，执行进行方式与通过 MSBuild 调用时的方式相同，但在引用项目方面存在差异。 在 MSBuild 中，需要引用项目时，实际上会发生生成；也就是说，它会运行任务和工具，并生成输出。 当 Visual Studio 生成查找引用项目时，MSBuild 仅返回所引用项目的预期输出；它允许 Visual Studio 控制其他项目的生成。 Visual Studio 确定生成顺序并单独调用 MSBuild（根据需要），所有这些操作都完全在 Visual Studio 控制下进行。

如果使用解决方案文件调用 MSBuild，情况又会有所不同，MSBuild 将解析解决方案文件，创建标准 XML 输入文件，对文件进行评估，然后作为项目执行文件。 解决方案生成在任何项目之前执行。 从 Visual Studio 生成时，不会出现这些情况；MSBuild 不会看到解决方案文件。 因此，解决方案生成自定义（使用 before.SolutionName.sln.targets 和 after.SolutionName.sln.targets）仅适用于 Msbuild.exe 或对象模型驱动，而不适用于 Visual Studio 生成。

### <a name="project-sdks"></a>项目 SDK

MSBuild 项目文件的 SDK 功能相对较新。 在进行此更改之前，项目文件显式导入了 .targets 和 .props 文件，这些文件为特定项目类型定义了生成过程。

.NET Core 项目导入适用于它们的 .NET SDK 版本。 请参阅概述 [.NET Core 项目 SDK](/dotnet/core/project-sdk/overview) 以及对[属性](/dotnet/core/project-sdk/msbuild-props)的引用。

## <a name="evaluation-phase"></a>评估阶段

本节讨论如何处理和分析这些输入文件，以生成确定将生成内容的内存中对象。

评估阶段的目的是基于输入 XML 文件和本地环境在内存中创建对象结构。 评估阶段包含五个处理输入文件（如项目 XML 文件或/和导入的 XML 文件（通常名 .props 或 .targets 文件））的环节，具体取决于它们主要是设置属性还是定义生成目标。 每个环节都会生成一部分内存中对象，这些对象稍后会在执行阶段用于生成项目，但在评估阶段不会发生实际的生成操作。 在每个环节中，将按照元素的显示顺序对其进行处理。

评估阶段中的各个环节如下：

- 评估环境变量
- 评估导入和属性
- 评估项定义
- 评估项
- 评估 [UsingTask](usingtask-element-msbuild.md) 元素
- 评估目标

这些环节的顺序有重大影响，在自定义项目文件时无比了解这一点。 请参阅[属性和项的评估顺序](comparing-properties-and-items.md#property-and-item-evaluation-order)。

### <a name="evaluate-environment-variables"></a>评估环境变量

在此阶段中，环境变量用于设置等效属性。 例如，PATH 环境变量可作为属性 `$(PATH)` 提供。 从命令行或脚本运行时，将正常使用命令环境，从 Visual Studio 运行时，将使用 Visual Studio 启动时生效的环境。

### <a name="evaluate-imports-and-properties"></a>评估导入和属性

在此阶段中，将读入整个输入 XML，包括项目文件和整个导入链。 MSBuild 创建一个内存中 XML 结构，该结构表示项目和所有导入文件的 XML。 此时，将对不在目标中的属性进行评估和设置。

由于 MSBuild 会在其进程中及早读取所有 XML 输入文件，因此在生成过程中对这些输入的任何更改都不会影响当前生成。

任何目标之外的属性的处理方式与目标中属性的处理方式不同。 在此阶段中，只评估在任何目标外部定义的属性。

由于属性在属性环节按顺序进行处理，因此输入中任何位置的属性都可以访问在输入中较早出现的属性值，但不能访问后面显示的属性。

由于在评估项之前处理属性，因此在属性环节的任何部分都不能访问任何项的值。 

### <a name="evaluate-item-definitions"></a>评估项定义

在此阶段中，将解释[项定义](item-definitions.md)，并创建这些定义的内存中表示形式。

### <a name="evaluate-items"></a>评估项

在目标内定义的项与任何目标外定义的项的处理方式不同。 在此阶段中，将处理任何目标之外的项及其关联的元数据。  由项定义设置的元数据将被项的元数据设置替代。 由于项按其显示的顺序进行处理，因此你可以引用之前定义的项，但不能引用后面显示的项。 因为项环节在属性环节之后，因此项都可以访问在任何目标外部定义的任何属性，无论稍后是否显示该属性定义。

### <a name="evaluate-usingtask-elements"></a>评估 `UsingTask` 元素

在此阶段中，将读取 [UsingTask](usingtask-element-msbuild.md) 元素，并声明这些任务以供稍后在执行阶段使用。

### <a name="evaluate-targets"></a>评估目标

在此阶段中，将在内存中创建所有目标对象结构，以准备执行。 无实际执行发生。 

## <a name="execution-phase"></a>执行阶段

在执行阶段，将对目标进行排序和运行，并执行所有任务。 但首先，在目标内定义的属性和项将以其显示顺序在单个阶段中进行评估。 处理顺序与不在目标中的属性和项的处理顺序截然不同：首先是所有属性，然后是在各个环节中的所有项。 对目标内的属性和项的更改可以在更改它们的目标之后观察到。

### <a name="target-build-order"></a>目标生成顺序

在单个项目中，目标按顺序执行。 核心问题在于如何确定生成所有内容的顺序，以便使用依赖项按正确顺序生成目标。  

目标生成顺序由每个目标上 `BeforeTargets`、`DependsOnTargets` 和 `AfterTargets` 属性的使用决定。 如果前面的目标修改了这些属性中引用的属性，则在执行前面的目标期间，后面的目标顺序会受到影响。

[确定目标生成顺序](target-build-order.md#determine-the-target-build-order)中介绍了排序规则。 此过程由包含要生成的目标的堆栈结构决定。 此任务顶部的目标将开始执行，如果它依赖于任何其他内容，则会将这些目标推送到堆栈顶部，并开始执行。  如果目标没有任何依赖项，则会执行到完成，并继续执行其父目标。

### <a name="project-references"></a>项目引用

MSBuild 可以采用两种代码路径，一种是此处描述的普通路径，一种是下一部分中所述的图形选项。

单个项目通过 `ProjectReference` 项来指定它们对其他项目的依赖性。 当堆栈顶部的项目开始生成时，它将达到 `ResolveProjectReferences` 目标的执行点，即在公用目标文件中定义的标准目标。

`ResolveProjectReferences` 使用 `ProjectReference` 项的输入调用 MSBuild 任务以获取输出。 `ProjectReference` 项转换为本地项，如 `Reference`。 当前项目的 MSBuild 执行阶段将暂停，同时执行阶段开始处理引用项目（根据需要先完成评估阶段）。 引用项目仅在你开始生成依赖项目后生成，因此，这会创建一个项目生成树。

Visual Studio 允许在解决方案 (.sln) 文件中创建项目依赖项。 依赖项是在解决方案文件中指定的，并且仅在生成解决方案或在 Visual Studio 内生成时才会考虑使用。 如果生成单个项目，则忽略此类型的依赖项。 解决方案引用由 MSBuild 转换为 `ProjectReference` 项，然后以相同的方式处理。

### <a name="graph-option"></a>图形选项

如果指定图形生成开关（`-graphBuild` 或 `-graph`），则 `ProjectReference` 会成为 MSBuild 使用的一级概念。 MSBuild 将分析所有项目并构造生成顺序图，即项目的实际依赖项关系图，然后遍历该关系图以确定生成顺序。 与单个项目中的目标一样，MSBuild 确保引用的项目是在其所依赖的项目之后生成的。

## <a name="parallel-execution"></a>并行执行

如果使用多处理器支持（`-maxCpuCount` 或 `-m` 开关），MSBuild 将创建节点，这些节点是使用可用 CPU 内核的 MSBuild 进程。 每个项目都被提交给一个可用节点。 在节点内，各个项目生成将按顺序执行。

可以通过设置布尔变量 <xref:Microsoft.Build.Tasks.MSBuild.BuildInParallel%2A> 为并行执行启用任务，该变量是根据 MSBuild 中 `$(BuildInParallel)` 属性的值设置的。 对于为并行执行启用的任务，工作计划程序会管理节点并将工作分配给节点。

请参阅[使用 MSBuild 并行生成多个项目](building-multiple-projects-in-parallel-with-msbuild.md)

## <a name="standard-imports"></a>标准导入

Microsoft.Common.props 和 Microsoft.Common.targets 都是由 .NET 项目文件导入的（在 SDK 样式项目中显式或隐式导入），并且位于 Visual Studio 安装的 MSBuild\Current\bin 文件夹中。 C++ 项目具有其自己的导入层次结构；请参阅 [C++ 项目的 MSBuild 内部层次结构](/cpp/build/reference/msbuild-visual-cpp-overview)。

Microsoft.Common.props 文件设置可重写的默认值。 它在项目文件的开头导入（显式或隐式）。 这样一来，项目设置将显示在默认值之后，这样就可以重写它们。

Microsoft.Common.targets 文件及其导入的目标文件定义 .NET 项目的标准生成过程。 它还提供了可用于自定义生成的扩展点。

在实现中，Microsoft.Common.targets 是一个导入 Microsoft.Common.CurrentVersion.targets 的精简包装器。 此文件包含标准属性设置，并定义可定义生成过程的实际目标。 此处定义 `Build` 目标，但实际上它是空的。 但 `Build` 目标包含 `DependsOn` 属性，该属性指定构成实际生成步骤的各个目标，这些步骤是 `BeforeBuild`、`CoreBuild` 和 `AfterBuild`。 `Build` 目标定义如下：

```xml
  <PropertyGroup>
    <BuildDependsOn>
      BeforeBuild;
      CoreBuild;
      AfterBuild
    </BuildDependsOn>
  </PropertyGroup>

  <Target
      Name="Build"
      Condition=" '$(_InvalidConfigurationWarning)' != 'true' "
      DependsOnTargets="$(BuildDependsOn)"
      Returns="@(TargetPathWithTargetPlatformMoniker)" />
```

`BeforeBuild` 和 `AfterBuild` 是扩展点。 它们在 Microsoft.Common.CurrentVersion.targets 文件中是空的，但项目可以提供自己的 `BeforeBuild` 和 `AfterBuild` 目标，其中包含需要在主生成过程之前或之后执行的任务。 `AfterBuild` 在无操作目标 `Build` 前运行，因为 `AfterBuild` 出现在 `Build` 目标的 `DependsOn` 属性中，但在 `CoreBuild` 之后发生。

`CoreBuild` 目标包含对生成工具的调用，如下所示：

```xml
  <PropertyGroup>
    <CoreBuildDependsOn>
      BuildOnlySettings;
      PrepareForBuild;
      PreBuildEvent;
      ResolveReferences;
      PrepareResources;
      ResolveKeySource;
      Compile;
      ExportWindowsMDFile;
      UnmanagedUnregistration;
      GenerateSerializationAssemblies;
      CreateSatelliteAssemblies;
      GenerateManifests;
      GetTargetPath;
      PrepareForRun;
      UnmanagedRegistration;
      IncrementalClean;
      PostBuildEvent
    </CoreBuildDependsOn>
  </PropertyGroup>
  <Target
      Name="CoreBuild"
      DependsOnTargets="$(CoreBuildDependsOn)">

    <OnError ExecuteTargets="_TimeStampAfterCompile;PostBuildEvent" Condition="'$(RunPostBuildEvent)'=='Always' or '$(RunPostBuildEvent)'=='OnOutputUpdated'"/>
    <OnError ExecuteTargets="_CleanRecordFileWrites"/>

  </Target>
```

下表对这些目标进行了说明；某些目标仅适用于某些项目类型。

| 目标 | 描述 |
|--------|-------------|
| BuildOnlySettings | 仅适用于实际生成的设置，而不适用于 Visual Studio 在项目加载时调用 MSBuild。 |
| PrepareForBuild | 准备生成的先决条件 |
| PreBuildEvent | 项目的扩展点，用于定义在生成之前要执行的任务 |
| ResolveProjectReferences | 分析项目依赖项并生成引用的项目 |
| ResolveAssemblyReferences| 找到引用的程序集。 |
| ResolveReferences | 包含 `ResolveProjectReferences` 和 `ResolveAssemblyReferences`，用于查找所有依赖项 |
| PrepareResources | 处理资源文件 |
| ResolveKeySource| 解析用于对程序集进行签名的强名称密钥以及用于对 [ClickOnce](../deployment/clickonce-security-and-deployment.md) 清单进行签名的证书。 |
| Compile | 调用编译器 |
| ExportWindowsMDFile | 基于编译器生成的 WinMDModule 文件生成 [WinMD](/uwp/winrt-cref/winmd-files) 文件。 |
| UnmanagedUnregistration | 从上一个生成中删除/清除 [COM 互操作](/dotnet/standard/native-interop/cominterop)注册表项 |
| GenerateSerializationAssemblies | 使用 [sgen.exe](/dotnet/standard/serialization/xml-serializer-generator-tool-sgen-exe) 生成 XML 序列化程序集。|
| CreateSatelliteAssemblies | 为资源中的每个唯一区域性创建一个附属程序集。 |
| 生成清单 | 生成 [ClickOnce](../deployment/clickonce-security-and-deployment.md) 应用程序和部署清单或本机清单。 |
| GetTargetPath | 使用元数据返回包含此项目的生成产品（可执行文件或程序集）的项。 |
| PrepareForRun | 将生成输出复制到最终目录（如果它们已更改）。 |
| UnmanagedRegistration | 设置 [COM 互操作](/dotnet/standard/native-interop/cominterop)的注册表项 |
| IncrementalClean | 删除在先前生成中生成但未在当前生成中生成的文件。 这是使 `Clean` 在增量生成中工作的必须条件。 |
| PostBuildEvent | 项目的扩展点，用于定义在生成之后运行的任务 |

上表中的许多目标都可在特定于语言的导入中找到，如 Microsoft.CSharp.targets。 此文件定义特定于 C# .NET 项目的标准生成过程中的步骤。 例如，它包含实际调用 C# 编译器的 `Compile` 目标。

## <a name="user-configurable-imports"></a>用户可配置的导入

除了标准导入外，还可以添加几个导入来自定义生成过程。

- Directory.Build.props
- Directory.Build.targets

这些文件由其下任何子文件夹中的任何项目的标准导入读入。 这通常是解决方案级别的设置，用于控制解决方案中的所有项目，但在文件系统中也可能更高，直至驱动器的根目录。

Directory.Build.props 文件由 Microsoft.Common.props 导入，因此项目文件中提供了其中定义的属性。 可以在项目文件中重新定义这些属性，以便基于每个项目自定义值。 将在项目文件后读入 Directory.Build.targets 文件。 它通常包含目标，但在这里，你还可以定义不希望个别项目重新定义的属性。

## <a name="customizations-in-a-project-file"></a>项目文件中的自定义项

当你在“解决方案资源管理器”、“属性”窗口或“项目属性”中进行更改时，Visual Studio 将更新项目文件，但你也可以通过直接编辑项目文件自行进行更改。

许多生成行为可以通过设置 MSBuild 属性进行配置，可以在项目本地设置的项目文件中进行，也可以按照前面部分所述，通过创建 Directory.Build.props 文件为项目和解决方案的整个文件夹全局设置属性。 对于命令行或脚本上的临时生成，还可以使用命令行上的 `/p` 选项为 MSBuild 的特定调用设置属性。 有关可设置的属性的信息，请参阅[常见的 MSBuild 项目属性](common-msbuild-project-properties.md)。

## <a name="next-steps"></a>后续步骤

除了在此描述的扩展点之外，MSBuild 进程还有其他几个扩展点。 请参阅[自定义生成](customize-your-build.md)。 以及[如何扩展 Visual Studio 生成过程](how-to-extend-the-visual-studio-build-process.md)。

## <a name="see-also"></a>请参阅

[MSBuild](msbuild.md)