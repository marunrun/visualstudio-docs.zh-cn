---
title: Visual C++ 项目扩展性
ms.date: 04/23/2019
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
author: corob-msft
ms.author: corob
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f9427895644686c5c3b50311c8a3ab3ee036a6f4
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862459"
---
# <a name="visual-studio-c-project-system-extensibility-and-toolset-integration"></a>Visual Studio c + + 项目系统扩展性和工具集集成

Visual C++ 项目系统用于 .vcxproj 文件。 它基于 [Visual Studio 公共项目系统 (CPS) ](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/Index.md) 并提供附加的 c + + 特定的扩展点，以便于实现新工具集、生成体系结构和目标平台的集成。

## <a name="c-msbuild-targets-structure"></a>C + + MSBuild 目标结构

所有 .vcxproj 文件将导入这些文件：

```xml
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.Default.props" />
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.props" />
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />
```

这些文件本身很少定义。 相反，它们会根据这些属性值导入其他文件：

- `$(ApplicationType)`

   示例： Windows 应用商店、Android、Linux

- `$(ApplicationTypeRevision)`

   这必须是有效的版本字符串，格式为 "主要. 次要 [. 版本 [. 修订号]"。

   示例：1.0、10.0.0。0

- `$(Platform)`

   用于记录原因的生成体系结构，名为 "平台"。

   示例： Win32、x86、x64、ARM

- `$(PlatformToolset)`

   示例： v140、v141、v141_xp、llvm

这些属性值指定根文件夹下的文件夹名称 `$(VCTargetsPath)` ：

> `$(VCTargetsPath)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;*应用程序类型*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(ApplicationType)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(ApplicationTypeRevision)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*适用*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(Platform)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*PlatformToolsets*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(PlatformToolset)` \
&nbsp;&nbsp;&nbsp;&nbsp;*适用*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(Platform)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*PlatformToolsets*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(PlatformToolset)`

`$(VCTargetsPath)` \\ *Platforms* \\ `$(ApplicationType)` 对于 Windows 桌面项目，在为空时使用平台文件夹。

### <a name="add-a-new-platform-toolset"></a>添加新平台工具集

若要为现有的 Win32 平台添加新的工具集（例如，"MyToolset"）， *MyToolset*请在 "平台 Win32 PlatformToolsets" 下创建一个 "MyToolset" 文件夹， `$(VCTargetsPath)` 并在其中创建 "*属性*" 和 "*工具集*" 文件* \\ \\ \\ \\ *。

" *PlatformToolsets* " 下的每个文件夹名称将作为指定平台的可用**平台工具集**出现在 "**项目属性**" 对话框中，如下所示：

!["项目属性页" 对话框中的 "平台工具集" 属性](media/vc-project-extensibility-platform-toolset-property.png ""项目属性页" 对话框中的 "平台工具集" 属性")

创建此工具集支持的每个现有平台文件夹*中的类似* *MyToolset* *文件夹和工具集。*

### <a name="add-a-new-platform"></a>添加新平台

若要添加新平台（例如 "MyPlatform"），请在 " *MyPlatform*平台 `$(VCTargetsPath)` * \\ \\ *" 下创建一个 MyPlatform 文件夹，并在其中创建*属性*、*属性*和*platform .targets*文件。 同时创建 `$(VCTargetsPath)` * \\ \\ 平台*<strong><em>MyPlatform</em></strong>* \\ PlatformToolsets \\ *文件夹，并在其中至少创建一个工具集。

每个文件夹的 " *平台* " 文件夹下的所有文件夹名称都 `$(ApplicationType)` `$(ApplicationTypeRevision)` 作为项目的可用 **平台** 选项显示在 IDE 中。

!["新建项目平台" 对话框中的新平台选项](media/vc-project-extensibility-new-project-platform.png ""新建项目平台" 对话框中的新平台选项")

### <a name="add-a-new-application-type"></a>添加新的应用程序类型

若要添加新的应用程序类型， *MyApplicationType*请在 " `$(VCTargetsPath)` * \\ 应用程序 \\ 类型*" 下创建 MyApplicationType 文件夹，并在其中创建一个*属性*文件。 应用程序类型至少需要一个修订版本，因此，请创建一个 `$(VCTargetsPath)` * \\ \\ MyApplicationType \\ 1.0 文件夹的应用程序类型*，并在其中创建一个*属性*文件。 还应创建 `$(VCTargetsPath)` * \\ ApplicationType \\ MyApplicationType \\ 1.0 \\ 平台*文件夹，并在其中至少创建一个平台。

`$(ApplicationType)` 和 `$(ApplicationTypeRevision)` 属性在用户界面中不可见。 它们是在项目模板中定义的，并且在创建项目后不能更改。

## <a name="the-vcxproj-import-tree"></a>.Vcxproj 导入树

Microsoft c + + 属性和目标文件的导入简化树如下所示：

> `$(VCTargetsPath)`\\*属性。* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(MSBuildExtensionsPath)`\\`$(MSBuildToolsVersion)`\\*属性* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportBefore* \\*默认值* \\ \* 。*属性* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*应用程序类型* \\ `$(ApplicationType)` \\*属性* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*应用程序* \\ `$(ApplicationType)` \\ 类型 `$(ApplicationTypeRevision)` \\*属性* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*应用程序* \\ `$(ApplicationType)` \\ 类型 `$(ApplicationTypeRevision)` \\*Platforms* \\ `$(Platform)` 平台 \\*属性* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportAfter* \\*默认值* \\ \* 。*属性*

Windows 桌面项目未定义 `$(ApplicationType)` ，因此它们只导入

> `$(VCTargetsPath)`\\*属性。* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(MSBuildExtensionsPath)`\\`$(MSBuildToolsVersion)`\\*属性* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportBefore* \\*默认值* \\ \* 。*属性* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Platforms* \\ `$(Platform)` 平台 \\*属性* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportAfter* \\*默认值* \\ \* 。*属性*

我们将使用 `$(_PlatformFolder)` 属性来保存 `$(Platform)` 平台文件夹位置。 此属性为

> `$(VCTargetsPath)`\\*适用*\\`$(Platform)`

对于 Windows 桌面应用程序和

> `$(VCTargetsPath)`\\*应用程序* \\ `$(ApplicationType)` \\ 类型 `$(ApplicationTypeRevision)` \\*平台*\\`$(Platform)`

对于其他所有内容。

将按以下顺序导入属性文件：

> `$(VCTargetsPath)`\\*属性* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*属性* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft 属性* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportBefore* \\ \* 。*属性* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*PlatformToolsets* \\ `$(PlatformToolset)` PlatformToolsets \\*工具集. 属性* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportAfter* \\ \* 。*属性*

目标文件按以下顺序导入：

> `$(VCTargetsPath)`\\*Microsoft .Cpp. 目标* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft .Cpp。* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Platform.string* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft .Cpp。* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportBefore* \\ \* 。*目标* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*PlatformToolsets* \\ `$(PlatformToolset)` PlatformToolsets \\*工具集. 目标* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportAfter* \\ \* 。*目标*

如果需要为工具集定义一些默认属性，可以将文件添加到相应的 ImportBefore 和 ImportAfter 文件夹。

## <a name="author-toolsetprops-and-toolsettargets-files"></a>创作工具集. 属性和工具集文件

使用此工具集时，*属性*和*工具集*文件可以完全控制在生成过程中所发生的情况。 它们还可以控制可用的调试器、某些 IDE 用户界面（如 " **属性页** " 对话框中的内容），以及项目行为的其他方面。

尽管工具集可以重写整个生成过程，但通常您只希望工具集修改或添加一些生成步骤，或使用不同的生成工具作为现有生成过程的一部分。 为实现此目标，工具集可以导入许多常见的属性和目标文件。 根据你希望工具集执行的操作，这些文件可能会很有用，可用作导入或示例：

- `$(VCTargetsPath)`\\*CppCommon*

  此文件定义本机生成过程的主要部分，并且还会导入：

  - `$(VCTargetsPath)`\\*CppBuild*

  - `$(VCTargetsPath)`\\*BuildSteps*

  - `$(MSBuildToolsPath)`\\*Microsoft Common。*

- `$(VCTargetsPath)`\\*属性。*

   设置使用 Microsoft 编译器和目标窗口的工具集的默认值。

- `$(VCTargetsPath)`\\*WindowsSDK. 属性*

   此文件确定 Windows SDK 位置，并为面向 Windows 的应用定义一些重要属性。

### <a name="integrate-toolset-specific-targets-with-the-default-c-build-process"></a>将工具集特定目标与默认 c + + 生成过程集成

*CppCommon*中定义了默认 c + + 生成过程。 目标不会调用任何特定的生成工具;它们指定主要的生成步骤、顺序和依赖项。

C + + 生成具有三个主要步骤，这些步骤由以下目标表示：

- `BuildGenerateSources`

- `BuildCompile`

- `BuildLink`

由于每个生成步骤都可以单独执行，因此，在一个步骤中运行的目标不能依赖在作为另一步骤的一部分运行的目标中定义的项组和属性。 此分部允许特定的生成性能优化。 尽管默认情况下不使用它，但仍鼓励您遵守这种分离。

在每个步骤内运行的目标受以下属性控制：

- `$(BuildGenerateSourcesTargets)`

- `$(BuildCompileTargets)`

- `$(BeforeBuildLinkTargets)`

每个步骤还具有前后属性。

```xml
<Target
  Name="_BuildGenerateSourcesAction"
  DependsOnTargets="$(CommonBuildOnlyTargets);$(BeforeBuildGenerateSourcesTargets);$(BuildGenerateSourcesTargets);$(AfterBuildGenerateSourcesTargets)" />

<Target
  Name="\_BuildCompileAction"
  DependsOnTargets="$(CommonBuildOnlyTargets);$(BeforeBuildCompileTargets);$(BuildCompileTargets);$(AfterBuildCompileTargets)" />

<Target
  Name="\_BuildLinkAction"
  DependsOnTargets="$(CommonBuildOnlyTargets);$(BeforeBuildLinkTargets);$(BuildLinkTargets);$(AfterBuildLinkTargets)" />
```

有关每个步骤中包含的目标的示例，请参阅 *CppBuild* 文件：

```xml
<BuildCompileTargets Condition="'$(ConfigurationType)'\!='Utility'">
  $(BuildCompileTargets);
  _ClCompile;
  _ResGen;
  _ResourceCompile;
  $(BuildLibTargets);
</BuildCompileTargets>
```

如果你查看目标（例如 `_ClCompile` ），你会发现它们不会直接执行任何操作，而是依赖于其他目标，包括 `ClCompile` ：

```xml
<Target Name="_ClCompile"
  DependsOnTargets="$(BeforeClCompileTargets);$(ComputeCompileInputsTargets);MakeDirsForCl;ClCompile;$(AfterClCompileTargets)" >
</Target>
```

`ClCompile` 和其他生成工具特定目标在 *CppBuild*中定义为空目标：

```xml
<Target Name="ClCompile"/>
```

由于 `ClCompile` 目标为空，除非它被工具集重写，否则不会执行实际的生成操作。 工具集目标可以重写 `ClCompile` 目标，也就是说，在 `ClCompile` 导入 *CppBuild*后，它们可以包含其他定义：

```xml
<Target Name="ClCompile"
  Condition="'@(ClCompile)' != ''"
  DependsOnTargets="SelectClCompile">
  <!-- call some MSBuild tasks -->
</Target>
```

尽管其名称是在 Visual Studio 实现跨平台支持之前创建的，但 `ClCompile` 目标不需要调用 CL.exe。 它还可以使用适当的 MSBuild 任务来调用 Clang、gcc 或其他编译器。

`ClCompile`目标不应具有任何依赖项 `SelectClCompile` （目标除外），这是在 IDE 中使用单个文件编译命令所必需的。

## <a name="msbuild-tasks-to-use-in-toolset-targets"></a>要在工具集目标中使用的 MSBuild 任务

若要调用实际的生成工具，目标需要调用 MSBuild 任务。 有一个基本的 [Exec 任务](../msbuild/exec-task.md) ，可用于指定要运行的命令行。 但是，生成工具通常有很多选项，即输入。 和输出用于跟踪增量生成，因此，对其进行特殊的任务会更有意义。 例如，任务将 `CL` MSBuild 属性转换为 CL.exe 开关，将它们写入响应文件，并调用 CL.exe。 它还跟踪所有输入和输出文件以供以后的增量生成。 有关详细信息，请参阅 [增量生成和最新检查](#incremental-builds-and-up-to-date-checks)。

Microsoft.Cpp.Common.Tasks.dll 实现以下任务：

- `BSCMake`

- `CL`

- `ClangCompile` (clang-gcc 交换机) 

- `LIB`

- `LINK`

- `MIDL`

- `Mt`

- `RC`

- `XDCMake`

- `CustomBuild` (例如 Exec，但具有输入和输出跟踪) 

- `SetEnv`

- `GetOutOfDateItems`

如果工具与现有工具执行相同的操作，并且具有类似的命令行开关 (如 clang-cl 和 CL do) ，则可以对这两种工具使用相同的任务。

如果需要为生成工具创建新任务，可以从以下选项中进行选择：

1. 如果你很少使用此任务，或者如果你的生成不重要，则可以使用 MSBuild "内联" 任务：

   - Xaml 任务 (自定义生成规则) 

     有关 Xaml 任务声明的示例，请参阅 `$(VCTargetsPath)` \\ *BuildCustomizations* \\ *masm.xml*及其用法，请参阅 `$(VCTargetsPath)` \\ *BuildCustomizations* \\ *masm*。

   - [代码任务](../msbuild/msbuild-inline-tasks.md)

1. 如果希望获得更好的任务性能或只需要更复杂的功能，请使用常规的 MSBuild [任务编写](../msbuild/task-writing.md) 过程。

   如果该工具的所有输入和输出都不会在工具命令行上列出（如 `CL` 、 `MIDL` 和事例）， `RC` 并且如果需要自动输入和输出文件跟踪并创建 tlog 文件，则从类派生任务 `Microsoft.Build.CPPTasks.TrackedVCToolTask` 。 目前，在存在基本 [ToolTask](/dotnet/api/microsoft.build.utilities.tooltask) 类的文档时，没有关于类详细信息的示例或文档 `TrackedVCToolTask` 。 如果这是特别感兴趣的，请将你的语音添加到 [developercommunity.visualstudio.com](https://developercommunity.visualstudio.com/spaces/62/index.html)上的请求。

## <a name="incremental-builds-and-up-to-date-checks"></a>增量生成和最新检查

默认的 MSBuild 增量生成目标使用 `Inputs` 和 `Outputs` 特性。 如果指定这些输入，则 MSBuild 仅在任何输入的时间戳比所有输出都有更新时才调用目标。 由于源文件通常包含或导入其他文件，并且生成工具会根据工具选项生成不同的输出，因此很难在 MSBuild 目标中指定所有可能的输入和输出。

为了解决此问题，c + + 生成使用了不同的技术来支持增量生成。 大多数目标不指定输入和输出，因此，在生成期间始终运行。 目标调用的任务将有关所有输入和输出的信息写入具有 tlog 扩展名的 *tlog* 文件中。 以后的版本将使用 tlog 文件来检查哪些内容已更改，需要重新生成以及哪些内容是最新的。 Tlog 文件也是 IDE 中默认生成最新检查的唯一源。

若要确定所有输入和输出，本机工具任务使用 tracker.exe 和 MSBuild 提供的 [FileTracker](/dotnet/api/microsoft.build.utilities.filetracker) 类。

Microsoft.Build.CPPTasks.Common.dll 定义 `TrackedVCToolTask` 公共抽象基类。 大多数本机工具任务都是从此类派生的。

从 Visual Studio 2017 更新15.8 开始，你可以使用 `GetOutOfDateItems` Microsoft.Cpp.Common.Tasks.dll 中实现的任务为具有已知输入和输出的自定义目标生成 tlog 文件。
或者，您可以使用任务创建它们 `WriteLinesToFile` 。 请参阅 `_WriteMasmTlogs` BuildCustomizations 中的目标 `$(VCTargetsPath)` \\ *BuildCustomizations* \\ *masm.targets*作为示例。

## <a name="tlog-files"></a>tlog 文件

有三种类型的 tlog 文件： *读取*、 *写入*和 *命令行*。 读取和写入 tlog 文件由增量生成和 IDE 中的最新检查使用。 命令行。 tlog 文件仅用于增量生成。

MSBuild 提供这些帮助器类来读取和写入 tlog 文件：

- [CanonicalTrackedInputFiles](/dotnet/api/microsoft.build.utilities.canonicaltrackedinputfiles)

- [CanonicalTrackedOutputFiles](/dotnet/api/microsoft.build.utilities.canonicaltrackedoutputfiles)

[FlatTrackingData](/dotnet/api/microsoft.build.utilities.flattrackingdata)类可用于访问读写 tlog 文件和标识比输出更新的输入，或者如果缺少输出，则为。 它在最新检查中使用。

命令行。 tlog 文件包含有关在生成中使用的命令行的信息。 它们仅用于增量生成，而不是最新的检查，因此内部格式由生成它们的 MSBuild 任务决定。

### <a name="read-tlog-format"></a>读取 tlog 格式

*读取* (的 tlog 文件。 \* 读取。 \*tlog) 包含有关源文件及其依赖项的信息。

位于行开头的插入符号 (**^**) 指示一个或多个源。 共享相同依赖项的源由竖线分隔 (**\|**) 。

依赖项文件在源之后列出，每个依赖项文件位于各自的行上。 所有文件名都是完整路径。

例如，假设你的项目源位于 *F： \\ test \\ ConsoleApplication1 \\ ConsoleApplication1*中。 如果源文件（ *Class1*）包含，

```cpp
#include "stdafx.h" //precompiled header
#include "Class1.h"
```

然后，该文件包含后跟两个依赖 *项的源文件* ：

```tlog
^F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\CLASS1.CPP
F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.PCH
F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\CLASS1.H
```

不需要以大写编写文件名，但对于某些工具来说，这是一个方便。

### <a name="write-tlog-format"></a>写入 tlog 格式

*写入* (\* 。 \*tlog) 文件连接源和输出。

位于行开头的插入符号 (**^**) 指示一个或多个源。 多个源通过竖线分隔 (**\|**) 。

从源生成的输出文件应在源后列出，每个输出文件位于各自的行上。 所有文件名必须是完整路径。

例如，对于具有额外的源文件 *Class1*的简单控制台应用程序项目 *，该文件* 可能包含以下内容：

```tlog
^F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CLASS1.OBJ|F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.OBJ|F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\STDAFX.OBJ
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.ILK
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.EXE
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.PDB
```

## <a name="design-time-build"></a>设计时生成

在 IDE 中，.vcxproj 项目使用一组 MSBuild 目标来获取项目的附加信息，并重新生成输出文件。 其中一些目标仅用于设计时生成，但其中许多目标都在常规生成和设计时生成中使用。

有关设计时生成的常规信息，请参阅适用于 [设计时生成](https://github.com/dotnet/project-system/blob/master/docs/design-time-builds.md)的 CPS 文档。 此文档仅部分适用于 Visual C++ 项目。

`CompileDesignTime` `Compile` 设计时生成文档中提到的和目标决不会为 .vcxproj 项目运行。 Visual C++ .vcxproj 项目使用不同的设计时目标来获取 IntelliSense 信息。

### <a name="design-time-targets-for-intellisense-information"></a>IntelliSense 信息的设计时目标

.Vcxproj 项目中使用的设计时目标是在 DesignTime 中定义的 `$(VCTargetsPath)` \\ *Microsoft.Cpp.DesignTime.targets*。

`GetClCommandLines`目标为 IntelliSense 收集编译器选项：

```xml
<Target
  Name="GetClCommandLines"
  Returns="@(ClCommandLines)"
  DependsOnTargets="$(DesignTimeBuildInitTargets);$(ComputeCompileInputsTargets)">
```

- `DesignTimeBuildInitTargets` -仅设计时目标，设计时生成初始化是必需的。 除此之外，这些目标会禁止某些常规的生成功能来提高性能。

- `ComputeCompileInputsTargets` -修改编译器选项和项的一组目标。 这些目标在设计时和常规生成中运行。

目标调用 `CLCommandLine` 任务来创建用于 IntelliSense 的命令行。 同样，不管名称如何，它不仅可以处理 CL 选项，还可以处理 Clang 和 gcc 选项。 编译器开关的类型由 `ClangMode` 属性控制。

目前，该任务生成的命令行 `CLCommandLine` 始终使用 CL 开关 (即使在 Clang 模式下也是如此) 因为 IntelliSense 引擎可以更轻松地对其进行分析。

如果要添加在编译之前运行的目标（无论是常规还是设计时），请确保它不会破坏设计时生成或影响性能。 测试目标的最简单方法是打开开发人员命令提示符并运行以下命令：

```
msbuild /p:SolutionDir=*solution-directory-with-trailing-backslash*;Configuration=Debug;Platform=Win32;BuildingInsideVisualStudio=true;DesignTimebuild=true /t:\_PerfIntellisenseInfo /v:d /fl /fileloggerparameters:PerformanceSummary \*.vcxproj
```

此命令将生成详细的生成日志 *，该日志包含*有关目标和结束任务的性能摘要。

请确保 `Condition ="'$(DesignTimeBuild)' != 'true'"` 在仅适用于常规生成而不适用于设计时生成的所有操作中使用。

### <a name="design-time-targets-that-generate-sources"></a>生成源的设计时目标

*默认情况下，对于桌面本机项目，此功能处于禁用状态，并且在缓存的项目中当前不支持此功能*。

如果为 `GeneratorTarget` 项目项定义了元数据，则在加载项目和更改源文件时，将自动运行目标。

::: moniker range="vs-2017"

例如，若要在 .xaml 文件中自动生成 .cpp 或 .h 文件，则 `$(VSInstallDir)` \\ *MSBuild* \\ *microsoft* \\ *WindowsXaml* \\ *v 15.0* \\ \* \\ *Microsoft.Windows.UI.Xaml.CPP.Targets*文件将定义这些实体，如下所示：

::: moniker-end

::: moniker range=">=vs-2019"

例如，若要在 .xaml 文件中自动生成 .cpp 或 .h 文件，则 `$(VSInstallDir)` \\ *MSBuild* \\ *microsoft* \\ *WindowsXaml* \\ *v 16.0* \\ \* \\ *Microsoft.Windows.UI.Xaml.CPP.Targets*文件将定义这些实体，如下所示：

::: moniker-end

```xml
<ItemDefinitionGroup>
  <Page>
    <GeneratorTarget>DesignTimeMarkupCompilation</GeneratorTarget>
  </Page>
  <ApplicationDefinition>
    <GeneratorTarget>DesignTimeMarkupCompilation</GeneratorTarget>
  </ApplicationDefinition>
</ItemDefinitionGroup>
<Target Name="DesignTimeMarkupCompilation">
  <!-- BuildingProject is used in Managed builds (always true in Native) -->
  <!-- DesignTimeBuild is used in Native builds (always false in Managed) -->
  <CallTarget Condition="'$(BuildingProject)' != 'true' Or $(DesignTimeBuild) == 'true'" Targets="DesignTimeMarkupCompilationCT" />
</Target>
```

若要使用 `Task.HostObject` 获取源文件的未保存内容，应将目标和任务注册为 .pkgdef 中给定项目的 [MsbuildHostObjects](/dotnet/api/microsoft.visualstudio.shell.interop.ivsmsbuildhostobject?view=visualstudiosdk-2017&preserve-view=true) ：

```reg
\[$RootKey$\\Projects\\{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}\\MSBuildHostObjects\]
\[$RootKey$\\Projects\\{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}\\MSBuildHostObjects\\DesignTimeMarkupCompilationCT;CompileXaml\]
@="{83046B3F-8984-444B-A5D2-8029DEE2DB70}"
```

## <a name="visual-c-project-extensibility-in-the-visual-studio-ide"></a>Visual Studio IDE 中的 Visual C++ 项目扩展性

Visual C++ 项目系统基于 [VS Project 系统](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/Index.md)，并使用其扩展点。 但是，项目层次结构实现特定于 Visual C++ 而不是基于 CPS，因此层次结构扩展性限制为项目项。

### <a name="project-property-pages"></a>项目属性页

有关常规设计信息，请参阅 [用于 VC + + 项目的框架多目标](https://devblogs.microsoft.com/visualstudio/framework-multi-targeting-for-vc-projects/)。

简而言之，在 c + + 项目的 " **项目属性** " 对话框中看到的属性页是由 *规则* 文件定义的。 规则文件指定要在属性页上显示的一组属性，以及它们在项目文件中的保存方式和位置。 规则文件是使用 Xaml 格式的 .xml 文件。 [XamlTypes](/dotnet/api/microsoft.build.framework.xamltypes)中介绍了用于对这些类型进行序列化的类型。 有关在项目中使用规则文件的详细信息，请参阅 [属性页 XML 规则文件](/cpp/build/reference/property-page-xml-files)。

规则文件必须添加到 `PropertyPageSchema` 项组：

```xml
<ItemGroup>
  <PropertyPageSchema Include="$(VCTargetsPath)$(LangID)\general.xml;"/>
  <PropertyPageSchema Include="$(VCTargetsPath)$(LangID)\general_file.xml">
    <Context>File</Context>
  </PropertyPageSchema>
</ItemGroup>
```

`Context` 元数据限制规则可见性，这也是由规则类型控制的，并且可以具有以下值之一：

`Project` | `File` | `PropertySheet`

CPS 支持上下文类型的其他值，但这些值不用于 Visual C++ 项目。

如果规则应该在多个上下文中可见，请使用分号 (**;**) 将上下文值隔开，如下所示：

```xml
<PropertyPageSchema Include="$(MyFolder)\MyRule.xml">
  <Context>Project;PropertySheet</Context>
</PropertyPageSchema>
```

#### <a name="rule-format-and-main-types"></a>规则格式和主要类型

规则格式很简单，因此本部分仅介绍影响规则在用户界面中的外观的属性。

```xml
<Rule
  Name="ConfigurationGeneral"
  DisplayName="General"
  PageTemplate="generic"
  Description="General"
  xmlns="http://schemas.microsoft.com/build/2009/properties">
```

`PageTemplate`特性定义规则在 "**属性页**" 对话框中的显示方式。 该属性可以具有以下值之一：

| 属性 | 说明 |
|------------| - |
| `generic` | 所有属性都显示在一页上的类别标题下面<br/>规则对 `Project` 和 `PropertySheet` 上下文可见，但不可见 `File` 。<br/><br/> 示例： `$(VCTargetsPath)` \\ *1033* \\ *general.xml* |
| `tool` | 类别显示为子页。<br/>此规则可在所有上下文中显示： `Project` 、 `PropertySheet` 和 `File` 。<br/>仅当项目具有中定义的项时，才会在项目属性中看到该规则 `ItemType` `Rule.DataSource` ，除非该规则名称包含在 `ProjectTools` 项组中。<br/><br/>示例： `$(VCTargetsPath)` \\ *1033* \\ *clang.xml* |
| `debugger` | 此页显示为 "调试" 页的一部分。<br/>当前忽略类别。<br/>规则名称应与调试启动器 MEF 对象的属性相匹配 `ExportDebugger` 。<br/><br/>示例： `$(VCTargetsPath)` \\ *1033* \\ *调试器 \_ 本地 \_windows.xml* |
| *客户* | 自定义模板。 模板的名称应与 `ExportPropertyPageUIFactoryProvider` MEF 对象的属性相匹配 `PropertyPageUIFactoryProvider` 。 请参阅 **VisualStudio. ProjectSystem. IPropertyPageUIFactoryProvider**。<br/><br/> 示例： `$(VCTargetsPath)` \\ *1033* \\ *userMacros.xml* |

如果规则使用基于属性网格的一个模板，则可以将这些扩展点用于其属性：

- [属性值编辑器](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/property_value_editors.md)

- [动态枚举值提供程序](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDynamicEnumValuesProvider.md)

#### <a name="extend-a-rule"></a>扩展规则

如果要使用现有规则，但需要添加或删除 (即，隐藏仅) 几个属性，则可以创建 [扩展规则](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/extending_rules.md)。

#### <a name="override-a-rule"></a>覆盖规则

也许您希望您的工具集使用大多数项目默认规则，而只是替换其中的一个或多个默认规则。 例如，假设您只想更改 C/c + + 规则以显示不同的编译器开关。 您可以向现有规则提供名称和显示名称相同的新规则，并在 `PropertyPageSchema` 导入默认 cpp 目标后将其包含在项组中。 在项目中只使用具有给定名称的一个规则，而包含在项组中的最后一个规则 `PropertyPageSchema` 入选。

#### <a name="project-items"></a>项目项

*ProjectItemsSchema.xml*文件定义 `ContentType` `ItemType` 被视为项目项的项的和值，并定义 `FileExtension` 元素以确定将新文件添加到的项组。

默认的 ProjectItemsSchema 文件位于 `$(VCTargetsPath)` \\ *1033* \\ *ProjectItemsSchema.xml*中。 若要对其进行扩展，必须创建一个具有新名称的架构文件，如 *MyProjectItemsSchema.xml*：

```xml
<ProjectSchemaDefinitions xmlns="http://schemas.microsoft.com/build/2009/properties">

  <ItemType Name="MyItemType" DisplayName="C/C++ compiler"/>

  <ContentType
    Name="MyItems"
    DisplayName="My items"
    ItemType=" MyItemType ">
  </ContentType>

  <FileExtension Name=".abc" ContentType=" MyItems"/>

</ProjectSchemaDefinitions>
```

然后在目标文件中添加：

```xml
<ItemGroup>
  <PropertyPageSchema Include="MyProjectItemsSchema.xml"/>
</ItemGroup>
```

示例： `$(VCTargetsPath)` \\ *BuildCustomizations* \\ *masm.xml*

### <a name="debuggers"></a>调试程序

Visual Studio 中的调试服务支持调试引擎的可扩展性。 有关详细信息，请参阅以下示例：

- [支持 lldb 调试的 MIEngine 开源项目](https://github.com/Microsoft/MIEngine)

- [Visual Studio 调试引擎示例](https://code.msdn.microsoft.com/windowsdesktop/Visual-Studio-Debug-Engine-c2e21c0e)

若要为调试会话指定调试引擎和其他属性，必须实现 [调试启动器](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDebugLaunchProvider.md) MEF 组件，并添加 `debugger` 规则。 有关示例，请参阅 `$(VCTargetsPath)` \\ 1033 \\ 调试器 \_ 本地 \_windows.xml 文件。

### <a name="deploy"></a>部署

。 .vcxproj 项目使用 Visual Studio 项目系统可扩展性来 [部署提供程序](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDeployProvider.md)。

### <a name="build-up-to-date-check"></a>生成最新检查

默认情况下，"生成最新" 检查需要在 `$(TlogLocation)` 生成过程中为所有生成输入和输出在此文件夹中创建 "读取" 和 "编写 tlog" 文件。

使用自定义最新检查：

1. 通过 `NoVCDefaultBuildUpToDateCheckProvider` 在 *工具集 .targets* 文件中添加功能，禁用默认的最新检查：

   ```xml
   <ItemGroup>
     <ProjectCapability Include="NoVCDefaultBuildUpToDateCheckProvider" />
   </ItemGroup>
   ```

1. 实现自己的 [IBuildUpToDateCheckProvider](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IBuildUpToDateCheckProvider.md)。

## <a name="project-upgrade"></a>项目升级

### <a name="default-vcxproj-project-upgrader"></a>.Vcxproj 项目升级程序

.Vcxproj 项目升级程序更改 `PlatformToolset` 、 `ApplicationTypeRevision` 、MSBuild 工具集版本和 .net framework。 最后两个将始终更改为 Visual Studio 版本默认设置，但 `PlatformToolset` `ApplicationTypeRevision` 可以由特殊的 MSBuild 属性控制。

升级程序使用这些条件来决定是否可以升级项目：

1. 对于定义和的 `ApplicationType` 项目 `ApplicationTypeRevision` ，有一个版本号高于当前文件夹的文件夹。

1. `_UpgradePlatformToolsetFor_<safe_toolset_name>`定义当前工具集的属性，并且其值不等于当前工具集。

   在这些属性名称中， *\<safe_toolset_name>* 表示工具集名称，其中所有非字母数字字符均替换为下划线 (**\_**) 。

当项目可以升级时，它参与了 *解决方案重定目标*。 有关详细信息，请参阅 [IVsTrackProjectRetargeting2](/dotnet/api/microsoft.visualstudio.shell.interop.ivstrackprojectretargeting2)。

如果要在 **解决方案资源管理器** 项目使用特定工具集时将项目名称修饰，请定义一个 `_PlatformToolsetShortNameFor_<safe_toolset_name>` 属性。

有关 `_UpgradePlatformToolsetFor_<safe_toolset_name>` 和 `_PlatformToolsetShortNameFor_<safe_toolset_name>` 属性定义的示例，请参阅 *属性* 文件。 有关用法的示例，请参阅 " `$(VCTargetPath)` \\ *Microsoft.*

### <a name="custom-project-upgrader"></a>自定义项目升级程序

若要使用自定义项目升级程序对象，请实现 MEF 组件，如下所示：

```csharp
/// </summary>
[Export("MyProjectUpgrader", typeof(IProjectRetargetHandler))]
[Export(typeof(IProjectRetargetHandler))]
[ExportMetadata("Name", "MyProjectUpgrader")]
[OrderPrecedence(20)]
[PartMetadata(ProjectCapabilities.Requires, ProjectCapabilities.VisualC)]

internal class MyProjectUpgrader: IProjectRetargetHandler
{
    // ...
}
```

你的代码可以导入和调用 .vcxproj 升级程序对象：

```csharp
// ...
[Import("VCDefaultProjectUpgrader")]
// ...
    IProjectRetargetHandler Lazy<IProjectRetargetHandler>
    VCDefaultProjectUpgrader { get; set; }
// ...
```

`IProjectRetargetHandler` 在 *Microsoft.VisualStudio.ProjectSystem.VS.dll* 中定义，并且类似于 `IVsRetargetProjectAsync` 。

定义 `VCProjectUpgraderObjectName` 属性，告知项目系统使用您的自定义升级程序对象：

```xml
<PropertyGroup>
  <VCProjectUpgraderObjectName>MyProjectUpgrader</VCProjectUpgraderObjectName>
</PropertyGroup>
```

#### <a name="disable-project-upgrade"></a>禁用项目升级

若要禁用项目升级，请使用 `NoUpgrade` 值：

```xml
<PropertyGroup>
  <VCProjectUpgraderObjectName>NoUpgrade</VCProjectUpgraderObjectName>
</PropertyGroup>
```

## <a name="project-cache-and-extensibility"></a>项目缓存和扩展性

为了在 Visual Studio 2017 中使用大型 c + + 解决方案时提高性能，引入了 [项目缓存](https://devblogs.microsoft.com/cppblog/faster-c-solution-load-with-vs-15/) 。 它实现为以项目数据填充的 SQLite 数据库，然后用于加载项目，而无需将 MSBuild 或 CPS 项目加载到内存中。

由于从缓存中加载的 .vcxproj 项目不存在 CPS 对象，因此将导入 `UnconfiguredProject` 或无法创建扩展的 MEF 组件 `ConfiguredProject` 。 为了支持可扩展性，当 Visual Studio 检测到项目使用 (或是否可能使用) MEF 扩展时，不会使用项目缓存。

这些项目类型始终完全加载并且在内存中具有 CPS 对象，因此会为其创建所有 MEF 扩展：

- 启动项目

- 具有自定义项目升级程序的项目，即定义 `VCProjectUpgraderObjectName` 属性

- 不以桌面窗口为目标的项目，即定义 `ApplicationType` 属性

- 共享项项目 ( .vcxitems) 和通过导入 .vcxitems 项目引用它们的任何项目。

如果未检测到上述任何条件，则会创建项目缓存。 缓存包括对 `get` 接口上的查询进行响应所需的 MSBuild 项目中的所有数据 `VCProjectEngine` 。 这意味着，由扩展完成的 MSBuild 属性和目标文件级别的所有修改都应在从缓存加载的项目中工作。

## <a name="shipping-your-extension"></a>寄送分机

有关如何创建 VSIX 文件的信息，请参阅 [发布 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)。 有关如何向特定安装位置添加文件（例如，在下添加文件）的信息， `$(VCTargetsPath)` 请参阅在 [extension 文件夹外部安装](../extensibility/set-install-root.md)。

## <a name="additional-resources"></a>其他资源

Microsoft 生成系统 ([MSBuild](../msbuild/msbuild.md)) 为项目文件提供生成引擎和基于 XML 的可扩展格式。 应熟悉基本的 [MSBuild 概念](../msbuild/msbuild-concepts.md) ，并了解 Visual C++ 的 [msbuild](/cpp/build/reference/msbuild-visual-cpp-overview) 如何工作才能扩展 Visual C++ 项目系统。

Managed Extensibility Framework ([MEF](/dotnet/framework/mef/)) 提供了 CPS 和 Visual C++ 项目系统所使用的扩展 api。 有关 CPS 如何使用 MEF 的概述，请参阅[VSProjectSystem 概述](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/mef.md)中的[cps 和 mef](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/mef.md#cps-and-mef) 。

您可以自定义现有生成系统以添加生成步骤或新的文件类型。 有关详细信息，请参阅 [MSBuild (Visual C++) 概述](/cpp/build/reference/msbuild-visual-cpp-overview) 和使用 [项目属性](/cpp/build/working-with-project-properties)。
