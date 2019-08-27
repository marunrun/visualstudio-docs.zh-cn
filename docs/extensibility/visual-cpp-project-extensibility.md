---
title: VisualC++项目扩展性
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
ms.openlocfilehash: 10869ad290b0b8df614d25d792d0b3ed1e88eb17
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825564"
---
# <a name="visual-studio-c-project-system-extensibility-and-toolset-integration"></a>Visual StudioC++项目系统可扩展性和工具集集成

视觉对象C++项目系统用于.vcxproj 文件。 它基于[Visual Studio 公共项目系统 (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/Index.md) ，并提供附加的C++轻松集成的新工具集的特定扩展点生成体系结构，并为目标平台。

## <a name="c-msbuild-targets-structure"></a>C++MSBuild 目标结构

所有.vcxproj 文件导都入这些文件：

```xml
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.Default.props" />
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.props" />
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />
```

这些文件定义少本身。 相反，它们导入这些属性值为基础的其他文件：

- `$(ApplicationType)`

   示例：Windows 应用商店、 Android、 Linux

- `$(ApplicationTypeRevision)`

   这必须是有效版本字符串，窗体 [.revision]]。

   示例：1.0, 10.0.0.0

- `$(Platform)`

   生成体系结构，出于历史原因，名为"平台"。

   示例：Win32 中，x86、 x64、 ARM

- `$(PlatformToolset)`

   示例： v140、 v141、 v141_xp、 llvm

这些属性值指定下的文件夹名称`$(VCTargetsPath)`根文件夹：

> `$(VCTargetsPath)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;*应用程序类型*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(ApplicationType)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(ApplicationTypeRevision)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*平台*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(Platform)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*PlatformToolsets*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(PlatformToolset)` \
&nbsp;&nbsp;&nbsp;&nbsp;*平台*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(Platform)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*PlatformToolsets*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(PlatformToolset)`

`$(VCTargetsPath)` \\*平台*\\使用文件夹时`$(ApplicationType)`为空，Windows 桌面项目。

### <a name="add-a-new-platform-toolset"></a>添加一个新的平台工具集

若要添加新的工具集，例如，"MyToolset"适用于现有的 Win32 平台，创建*MyToolset*下的文件夹`$(VCTargetsPath)` *\\平台\\Win32\\PlatformToolsets\\* ，并创建*Toolset.props*并*Toolset.targets*中它的文件。

在每个文件夹名称*PlatformToolsets*将出现在**项目属性**为可用的对话框**平台工具集**为指定的平台，如下所示：

![在项目属性页对话框中的平台工具集属性](media/vc-project-extensibility-platform-toolset-property.png "项目属性页对话框中的平台工具集属性")

创建类似*MyToolset*文件夹并*Toolset.props*并*Toolset.targets*此工具集支持每个现有平台文件夹中的文件。

### <a name="add-a-new-platform"></a>添加新的平台

若要添加新的平台，例如，"MyPlatform"，创建*MyPlatform*下的文件夹`$(VCTargetsPath)` *\\平台\\* ，并创建*Platform.default.props*， *Platform.props*，和*Platform.targets*中它的文件。 此外创建`$(VCTargetsPath)` *\\平台\\* <strong><em>MyPlatform</em></strong> *\\PlatformToolsets\\* 文件夹，并在其中创建至少一个工具集。

下的所有文件夹名称*平台*每个文件夹`$(ApplicationType)`并`$(ApplicationTypeRevision)`为可在 IDE 中显示**平台**项目的选项。

![在新建项目平台对话框中的新的平台选择](media/vc-project-extensibility-new-project-platform.png "新选择的平台，在新建项目平台对话框")

### <a name="add-a-new-application-type"></a>添加新的应用程序类型

若要添加新的应用程序类型，创建*MyApplicationType*下的文件夹`$(VCTargetsPath)` *\\应用程序类型\\* 并创建*Defaults.props*文件中的。 至少一个修订版本是必需的应用程序类型，因此创建`$(VCTargetsPath)` *\\应用程序类型\\MyApplicationType\\1.0*文件夹，并创建*Defaults.props*中该文件。 您还应创建`$(VCTargetsPath)`  *\\ApplicationType\\MyApplicationType\\1.0\\平台*文件夹并在其中创建至少一个平台。

`$(ApplicationType)` 和`$(ApplicationTypeRevision)`属性用户界面中不可见。 它们在项目模板中定义和创建项目后，不能更改。

## <a name="the-vcxproj-import-tree"></a>.Vcxproj 导入树

Microsoft 的导入的简化的树C++属性和目标文件如下所示：

> `$(VCTargetsPath)`\\*Microsoft.Cpp.Default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(MSBuildExtensionsPath)`\\`$(MSBuildToolsVersion)`\\*Microsoft.Common.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportBefore*\\*默认*\\\*。*属性* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*应用程序类型*\\`$(ApplicationType)`\\*Default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*应用程序类型*\\`$(ApplicationType)`\\`$(ApplicationTypeRevision)`\\*Default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*应用程序类型*\\`$(ApplicationType)`\\`$(ApplicationTypeRevision)`\\*平台*\\ `$(Platform)` \\ *Platform.default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportAfter*\\*默认*\\\*。*属性*

Windows 桌面项目不定义`$(ApplicationType)`，因此它们只能导入

> `$(VCTargetsPath)`\\*Microsoft.Cpp.Default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(MSBuildExtensionsPath)`\\`$(MSBuildToolsVersion)`\\*Microsoft.Common.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportBefore*\\*默认*\\\*。*属性* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Platforms*\\`$(Platform)`\\*Platform.default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportAfter*\\*默认*\\\*。*属性*

我们将使用`$(_PlatformFolder)`属性，包含`$(Platform)`平台文件夹位置。 此属性是

> `$(VCTargetsPath)`\\*平台*\\`$(Platform)`

对于 Windows 桌面应用，并

> `$(VCTargetsPath)`\\*应用程序类型*\\`$(ApplicationType)`\\`$(ApplicationTypeRevision)`\\*平台*\\`$(Platform)`

对于其他所有情况。

按以下顺序导入属性文件：

> `$(VCTargetsPath)`\\*Microsoft.Cpp.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Platform.props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft.Cpp.Platform.props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportBefore*\\\*.*props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*PlatformToolsets*\\`$(PlatformToolset)`\\*Toolset.props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportAfter*\\\*。*属性*

按以下顺序导入目标文件：

> `$(VCTargetsPath)`\\*Microsoft.Cpp.targets* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft.Cpp.Current.targets* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Platform.targets* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft.Cpp.Platform.targets* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportBefore*\\\*。*目标* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*PlatformToolsets*\\`$(PlatformToolset)`\\*Toolset.target* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportAfter*\\\*。*目标*

如果您需要定义您的工具集的某些默认属性，您可以将文件添加到相应 ImportBefore 和 ImportAfter 文件夹中。

## <a name="author-toolsetprops-and-toolsettargets-files"></a>作者 Toolset.props 和 Toolset.targets 文件

*Toolset.props*并*Toolset.targets*文件具有完全控制时会发生什么情况在生成期间使用此工具集。 它们还可以控制可用调试程序，某些 IDE 用户界面，例如中的内容**属性页**对话框中，以及一些其他方面的项目的行为。

尽管一个工具集，可以重写整个生成过程，但通常您只需要您修改或添加一些生成的步骤，或作为现有的生成过程的一部分使用不同的生成工具的工具集。 若要实现此目标，有多个常见的属性和目标文件可以导入您的工具集。 具体取决于您所需工具集来执行这些文件可能很有用的导入或作为示例：

- `$(VCTargetsPath)`\\*Microsoft.CppCommon.targets*

  此文件定义的本机生成过程中的主要部分，并还会导入：

  - `$(VCTargetsPath)`\\*Microsoft.CppBuild.targets*

  - `$(VCTargetsPath)`\\*Microsoft.BuildSteps.targets*

  - `$(MSBuildToolsPath)`\\*Microsoft.Common.Targets*

- `$(VCTargetsPath)`\\*Microsoft.Cpp.Common.props*

   设置使用 Microsoft 编译器和面向 Windows 的工具集的默认值。

- `$(VCTargetsPath)`\\*Microsoft.Cpp.WindowsSDK.props*

   此文件将确定 Windows SDK 的位置，并定义面向 Windows 的应用程序的某些重要属性。

### <a name="integrate-toolset-specific-targets-with-the-default-c-build-process"></a>将特定于工具集的目标集成，默认值C++生成过程

默认值C++中定义生成过程*Microsoft.CppCommon.targets*。 存在的目标不调用任何特定的生成工具;它们指定了主构建步骤中，其顺序和依赖项。

C++生成具有三个主要步骤，由以下目标：

- `BuildGenerateSources`

- `BuildCompile`

- `BuildLink`

因为可能会单独执行每个生成步骤，在一个步骤中运行的目标不能依赖项组并作为不同步骤的一部分运行的目标中定义的属性。 这种划分允许某些生成的性能优化。 尽管默认情况下不使用它，但仍建议您遵循这种分离。

由这些属性控制在每个步骤中运行的目标：

- `$(BuildGenerateSourcesTargets)`

- `$(BuildCompileTargets)`

- `$(BeforeBuildLinkTargets)`

每个步骤还具有 Before 和 After 属性。

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

请参阅*Microsoft.CppBuild.targets*文件中的每个步骤包含目标的示例：

```xml
<BuildCompileTargets Condition="'$(ConfigurationType)'\!='Utility'">
  $(BuildCompileTargets);
  _ClCompile;
  _ResGen;
  _ResourceCompile;
  $(BuildLibTargets);
</BuildCompileTargets>
```

如果您查看目标，如`_ClCompile`，你将看到它们不执行任何操作直接通过本身，但改为依赖于其他目标包括`ClCompile`:

```xml
<Target Name="_ClCompile"
  DependsOnTargets="$(BeforeClCompileTargets);$(ComputeCompileInputsTargets);MakeDirsForCl;ClCompile;$(AfterClCompileTargets)" >
</Target>
```

`ClCompile` 和其他生成特定于工具的目标定义为中的空目标*Microsoft.CppBuild.targets*:

```xml
<Target Name="ClCompile"/>
```

因为`ClCompile`目标为空，除非它一个工具集被重写，不执行任何实际生成操作。 工具集目标可以重写`ClCompile`目标，也就是说，它们可以包含另一个`ClCompile`定义导入后的*Microsoft.CppBuild.targets*:

```xml
<Target Name="ClCompile"
  Condition="'@(ClCompile)' != ''"
  DependsOnTargets="SelectClCompile">
  <!-- call some MSBuild tasks -->
</Target>
```

尽管其名称如此，这创建的 Visual Studio 实现跨平台支持之前，`ClCompile`目标不一定要调用 CL.exe。 它还可以通过使用相应的 MSBuild 任务调用 Clang、 gcc 高级版或其他编译器。

`ClCompile`目标不应具有任何依赖项除外`SelectClCompile`目标所需的单个文件编译命令，以便在 IDE 中。

## <a name="msbuild-tasks-to-use-in-toolset-targets"></a>若要使用的工具集目标中的 MSBuild 任务

若要调用的实际生成工具，需要调用 MSBuild 任务目标。 没有基本[Exec 任务](../msbuild/exec-task.md)，可以指定要运行的命令行。 但是，生成工具通常有很多选项，输入。 和跟踪的增量生成，以便它可以互通有无，它们具有特殊任务的输出。 例如，`CL`任务 CL.exe 交换机转换为 MSBuild 属性，将其写入到响应文件中，并且调用 CL.exe。 它还跟踪更高版本的增量生成的所有输入和输出文件。 有关详细信息，请参阅[增量生成和最新检查](#incremental-builds-and-up-to-date-checks)。

Microsoft.Cpp.Common.Tasks.dll 实现这些任务：

- `BSCMake`

- `CL`

- `ClangCompile` （clang gcc 开关）

- `LIB`

- `LINK`

- `MIDL`

- `Mt`

- `RC`

- `XDCMake`

- `CustomBuild` （输入和输出跟踪，但如 Exec）

- `SetEnv`

- `GetOutOfDateItems`

如果有工具执行相同的操作的现有工具和 （和相同 clang cl 和 CL） 具有类似的命令行开关，则可以对这两个使用相同的任务。

如果需要创建新任务的生成工具，可以从以下选项中进行选择：

1. 如果你使用此任务很少，或为生成无关紧要几秒钟后，可以使用 MSBuild inline 任务：

   - Xaml 任务 （自定义生成规则）

     有关 Xaml 任务声明一个示例，请参阅`$(VCTargetsPath)` \\ *BuildCustomizations*\\*masm.xml*，以及有关其用法，请参阅`$(VCTargetsPath)` \\*BuildCustomizations*\\*masm.targets*。

   - [代码任务](../msbuild/msbuild-inline-tasks.md)

1. 如果希望更好的任务性能或只是需要更复杂的功能，使用正则 MSBuild[任务写入](../msbuild/task-writing.md)过程。

   如果不是所有输入和输出的工具，工具命令行都列出作为 in `CL`， `MIDL`，和`RC`情况下，并且如果你希望自动输入和输出文件跟踪和.tlog 文件创建，则会将您的任务派生`Microsoft.Build.CPPTasks.TrackedVCToolTask`类。 目前，基的文档时[ToolTask](/dotnet/api/microsoft.build.utilities.tooltask)类中，没有任何示例或文档有关的详细信息`TrackedVCToolTask`类。 如果这会特别感兴趣，您的声音的请求上添加[developercommunity.visualstudio.com](https://developercommunity.visualstudio.com/spaces/62/index.html)。

## <a name="incremental-builds-and-up-to-date-checks"></a>增量生成和最新检查

默认 MSBuild 增量生成目标将使用`Inputs`和`Outputs`属性。 如果你指定它们，MSBuild 会调用目标仅当任何输入的所有输出比更高版本的时间戳。 源代码文件通常包括或导入其他文件和生成工具生成不同的输出，具体取决于工具选项，因为它很难指定所有可能的输入和 MSBuild 目标中的输出。

若要管理此问题，C++生成使用另一种技术来支持增量生成。 大多数目标没有指定输入和输出，并因此，始终在生成过程进行。 调用的目标的任务编写所有信息输入，并将输出到*tlog* .tlog 扩展名的文件。 .Tlog 文件由更高版本生成，以检查内容已更改，并且需要重新生成，并且什么是最新状态。 .Tlog 文件也是默认生成最新检查在 IDE 中的唯一来源。

若要确定所有输入和输出，本机工具任务使用 tracker.exe 并[FileTracker](/dotnet/api/microsoft.build.utilities.filetracker) MSBuild 提供的类。

Microsoft.Build.CPPTasks.Common.dll 定义`TrackedVCToolTask`公共抽象基类。 大部分本机工具任务都派生自此类。

从 Visual Studio 2017 更新 15.8 开始，你可以使用`GetOutOfDateItems`Microsoft.Cpp.Common.Tasks.dll 以生成具有已知的输入和输出的自定义目标的.tlog 文件中实现的任务。
或者，可以通过使用创建它们`WriteLinesToFile`任务。 请参阅`_WriteMasmTlogs`中的 target `$(VCTargetsPath)` \\ *BuildCustomizations*\\*masm.targets*作为示例。

## <a name="tlog-files"></a>.tlog 文件

有三种类型的.tlog 文件：*读取*，*编写*，并*命令行*。 读取和写入的.tlog 文件使用增量生成以及通过在 IDE 中最新的检查。 增量生成仅用于命令行的.tlog 文件。

MSBuild 提供了这些帮助器类读取和写入.tlog 文件：

- [CanonicalTrackedInputFiles](/dotnet/api/microsoft.build.utilities.canonicaltrackedinputfiles)

- [CanonicalTrackedOutputFiles](/dotnet/api/microsoft.build.utilities.canonicaltrackedoutputfiles)

[FlatTrackingData](/dotnet/api/microsoft.build.utilities.flattrackingdata)类可用于访问这两个读取和写入.tlog 文件，并确定新的文件不是输出，或缺少输出的输入。 最新检查中使用。

命令行的.tlog 文件包含在生成中使用命令行有关的信息。 它们仅用于增量生成，不是最新检查，因此内部格式由生成它们的 MSBuild 任务。

### <a name="read-tlog-format"></a>阅读的.tlog 格式

*读取*.tlog 文件 (\*.read。\*。tlog) 包含有关源文件及其依赖项的信息。

插入符号 ( **^** ) 在行开头指示一个或多个源。 共享同一个依赖项的源由竖线分隔 ( **\|** )。

之后的源，每个在其对应行中列出了依赖项文件。 所有文件的名称都是完整路径。

例如，假设你项目的源中找到*f:\\测试\\ConsoleApplication1\\ConsoleApplication1*。 如果在源文件*Class1.cpp*，具有这些包含，

```cpp
#include "stdafx.h" //precompiled header
#include "Class1.h"
```

然后*CL.read.1.tlog*文件包含后跟其两个依赖项的源文件：

```tlog
^F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\CLASS1.CPP
F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.PCH
F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\CLASS1.H
```

它不需要编写文件名称以大写形式，但它的一些工具提供了便利。

### <a name="write-tlog-format"></a>编写.tlog 格式

*编写*.tlog (\*.write。\*。tlog) 文件连接源和输出。

插入符号 ( **^** ) 在行开头指示一个或多个源。 由竖线分隔多个源 ( **\|** )。

将源中生成的输出文件应该列出后的源，每个在其对应行。 所有文件名称必须都是完整路径。

例如，对于具有的其他源文件的简单控制台应用程序项目*Class1.cpp*，则*link.write.1.tlog*文件可能包含：

```tlog
^F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CLASS1.OBJ|F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.OBJ|F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\STDAFX.OBJ
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.ILK
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.EXE
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.PDB
```

## <a name="design-time-build"></a>设计时生成

在 IDE 中，.vcxproj 项目使用一的组 MSBuild 目标，若要从项目中获取的其他信息以及重新生成输出文件。 仅在设计时生成中使用这些目标的某些，但其中的许多用于常规生成和设计时生成。

有关设计时生成的常规信息，请参阅的 CPS 文档[设计时生成](https://github.com/dotnet/project-system/blob/master/docs/design-time-builds.md)。 本文档才一定程度上适用于视觉对象C++项目。

`CompileDesignTime`和`Compile`设计时中所述的目标生成文档的.vcxproj 项目永远不会运行。 Visual C++ .vcxproj 项目使用不同的设计时目标来获取 IntelliSense 信息。

### <a name="design-time-targets-for-intellisense-information"></a>IntelliSense 信息的设计时目标

在.vcxproj 项目中使用的设计时目标中定义`$(VCTargetsPath)` \\ *Microsoft.Cpp.DesignTime.targets*。

`GetClCommandLines`目标收集用于 IntelliSense 的编译器选项：

```xml
<Target
  Name="GetClCommandLines"
  Returns="@(ClCommandLines)"
  DependsOnTargets="$(DesignTimeBuildInitTargets);$(ComputeCompileInputsTargets)">
```

- `DesignTimeBuildInitTargets` – 设计时仅生成目标，所需的设计时初始化。 此外，这些目标禁用某些常规生成功能，以改善性能。

- `ComputeCompileInputsTargets` -修改编译器选项和项的一组目标。 在设计时和常规生成中运行这些目标。

目标调用`CLCommandLine`任务以创建要用于 IntelliSense 的命令行。 同样，尽管其名称如此，它可以处理不仅 CL 选项，而且还 Clang 和 gcc 高级版选项。 编译器开关的类型由控制`ClangMode`属性。

目前，在命令行生成`CLCommandLine`任务始终使用 CL 开关 （即使在 Clang 模式下） 因为它们要分析的 IntelliSense 引擎更容易。

如果你要添加的目标之前编译、 运行是否定期或设计时，确保它不会中断的设计时生成，或会影响性能。 若要测试你的目标的最简单方法是打开开发人员命令提示符并运行以下命令：

```
msbuild /p:SolutionDir=*solution-directory-with-trailing-backslash*;Configuration=Debug;Platform=Win32;BuildingInsideVisualStudio=true;DesignTimebuild=true /t:\_PerfIntellisenseInfo /v:d /fl /fileloggerparameters:PerformanceSummary \*.vcxproj
```

此命令将生成详细的生成日志*msbuild.log*，末尾具有性能摘要的目标和任务。

请务必使用`Condition ="'$(DesignTimeBuild)' != 'true'"`中仅有意义的定期生成而不是针对设计时生成的所有操作。

### <a name="design-time-targets-that-generate-sources"></a>生成源的设计时目标

*此功能默认情况下，对于桌面本机项目处于禁用状态，当前不支持缓存项目*。

如果`GeneratorTarget`项目项定义元数据，目标运行自动加载该项目是和更改的源文件时。

::: moniker range="vs-2017"

例如，若要自动生成.cpp 或.h 文件从.xaml 文件`$(VSInstallDir)` \\ *MSBuild*\\*Microsoft* \\ *WindowsXaml*\\*v15.0*\\\*\\*Microsoft.Windows.UI.Xaml.CPP.Targets*文件定义这些实体：

::: moniker-end

::: moniker range=">=vs-2019"

例如，若要自动生成.cpp 或.h 文件从.xaml 文件`$(VSInstallDir)` \\ *MSBuild*\\*Microsoft* \\ *WindowsXaml*\\*v16.0*\\\*\\*Microsoft.Windows.UI.Xaml.CPP.Targets*文件定义这些实体：

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

若要使用`Task.HostObject`若要获取源代码文件的未保存的内容，目标和任务应注册为[MsbuildHostObjects](/dotnet/api/microsoft.visualstudio.shell.interop.ivsmsbuildhostobject?view=visualstudiosdk-2017) pkgdef 中给定的项目：

```reg
\[$RootKey$\\Projects\\{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}\\MSBuildHostObjects\]
\[$RootKey$\\Projects\\{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}\\MSBuildHostObjects\\DesignTimeMarkupCompilationCT;CompileXaml\]
@="{83046B3F-8984-444B-A5D2-8029DEE2DB70}"
```

## <a name="visual-c-project-extensibility-in-the-visual-studio-ide"></a>VisualC++项目中 Visual Studio IDE 可扩展性

视觉对象C++项目系统基于[VS 项目系统](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/Index.md)，并使用其可扩展性点。 但是，项目层次结构实现是特定于视觉对象C++而不基于 CPS，因此层次结构可扩展性空间限制为项目项。

### <a name="project-property-pages"></a>项目属性页

常规设计信息，请参阅[Framework 多目标的 VC + + 项目](https://devblogs.microsoft.com/visualstudio/framework-multi-targeting-for-vc-projects/)。

简单来说，属性页中看到**项目属性**对话框C++定义项目*规则*文件。 规则文件指定要显示在属性页上，以及如何在项目中保存的位置和文件属性的集。 规则文件是使用 Xaml 格式的.xml 文件。 使用其进行序列化的类型所述[Microsoft.Build.Framework.XamlTypes](/dotnet/api/microsoft.build.framework.xamltypes)。 有关使用项目中的规则文件的详细信息，请参阅[属性页 XML 规则文件](/cpp/build/reference/property-page-xml-files)。

必须将规则文件添加到`PropertyPageSchema`项组：

```xml
<ItemGroup>
  <PropertyPageSchema Include="$(VCTargetsPath)$(LangID)\general.xml;"/>
  <PropertyPageSchema Include="$(VCTargetsPath)$(LangID)\general_file.xml">
    <Context>File</Context>
  </PropertyPageSchema>
</ItemGroup>
```

`Context` 元数据限制规则的可见性，它还受规则类型，并可以具有下列值之一：

`Project` | `File` | `PropertySheet`

CPS 上下文类型支持其他值，但它们未在视觉对象中使用C++项目。

如果该规则应在多个上下文中可见，则使用分号 ( **;** ) 来分隔的上下文值，如下所示：

```xml
<PropertyPageSchema Include="$(MyFolder)\MyRule.xml">
  <Context>Project;PropertySheet</Context>
</PropertyPageSchema>
```

#### <a name="rule-format-and-main-types"></a>规则格式以及主要类型

规则格式是非常简单，因此本部分仅介绍影响在用户界面中规则的外观的属性。

```xml
<Rule
  Name="ConfigurationGeneral"
  DisplayName="General"
  PageTemplate="generic"
  Description="General"
  xmlns="http://schemas.microsoft.com/build/2009/properties">
```

`PageTemplate`属性定义了该规则中的显示方式**属性页**对话框。 该属性可以具有下列值之一：

| 特性 | 描述 |
|------------| - |
| `generic` | 在类别标题下一页上将显示所有属性<br/>规则可以对可见`Project`并`PropertySheet`上下文中，但不是`File`。<br/><br/> 示例:`$(VCTargetsPath)`\\*1033*\\*general.xml* |
| `tool` | 作为子页显示类别。<br/>规则可以在所有上下文中可见： `Project`，`PropertySheet`和`File`。<br/>仅当项目具有与项目的规则是在项目属性中可见`ItemType`中定义`Rule.DataSource`，除非中包含的规则名`ProjectTools`项组。<br/><br/>示例:`$(VCTargetsPath)`\\*1033*\\*clang.xml* |
| `debugger` | 页面会显示为调试页的一部分。<br/>当前忽略类别。<br/>规则名称应匹配的调试启动程序 MEF 对象`ExportDebugger`属性。<br/><br/>示例:`$(VCTargetsPath)`\\*1033*\\*debugger\_local\_windows.xml* |
| *custom* | 自定义模板。 模板的名称应与匹配`ExportPropertyPageUIFactoryProvider`属性的`PropertyPageUIFactoryProvider`MEF 对象。 请参阅**Microsoft.VisualStudio.ProjectSystem.Designers.Properties.IPropertyPageUIFactoryProvider**。<br/><br/> 示例:`$(VCTargetsPath)`\\*1033*\\*userMacros.xml* |

如果该规则使用基于属性网格的模板之一，它可以为其属性来使用这些扩展点：

- [属性值编辑器](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/property_value_editors.md)

- [动态枚举值提供程序](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDynamicEnumValuesProvider.md)

#### <a name="extend-a-rule"></a>扩展规则

如果你想要使用现有的规则，但需要添加或删除 （即，隐藏） 只需几个属性，可以创建[扩展规则](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/extending_rules.md)。

#### <a name="override-a-rule"></a>重写规则

您可能希望您的工具集使用的大多数项目默认规则，而是替换只是一个或多个这些。 例如，假设你只想要更改 C /C++规则，以显示不同的编译器开关。 可以提供新规则具有相同名称和显示名称与现有的规则，并将其包含在`PropertyPageSchema`项组的默认 cpp 目标导入之后。 在项目中，使用只有一个具有给定名称的规则和最后一个包含到`PropertyPageSchema`项组 wins。

#### <a name="project-items"></a>项目项

*ProjectItemsSchema.xml*文件定义`ContentType`并`ItemType`将被视为项目项的项的值，并定义`FileExtension`元素以确定新文件添加到的项组。

默认 ProjectItemsSchema 文件中找到`$(VCTargetsPath)` \\ *1033年*\\*ProjectItemsSchema.xml*。 若要扩展它，您必须创建架构文件使用新名称，例如*MyProjectItemsSchema.xml*:

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

然后在目标文件中，添加：

```xml
<ItemGroup>
  <PropertyPageSchema Include="MyProjectItemsSchema.xml"/>
</ItemGroup>
```

示例:`$(VCTargetsPath)`\\*BuildCustomizations*\\*masm.xml*

### <a name="debuggers"></a>调试器

在 Visual Studio 中的调试服务的调试引擎支持可扩展性。 有关详细信息，请参阅这些示例：

- [MIEngine，开放源代码项目，支持 lldb 调试](https://github.com/Microsoft/MIEngine)

- [Visual Studio 调试引擎示例](https://code.msdn.microsoft.com/windowsdesktop/Visual-Studio-Debug-Engine-c2e21c0e)

若要为调试会话指定的调试引擎和其他属性，则必须实现[调试启动器](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDebugLaunchProvider.md)MEF 组件，并添加`debugger`规则。 有关示例，请参阅`$(VCTargetsPath)` \\1033年\\调试器\_本地\_windows.xml 文件。

### <a name="deploy"></a>部署

.vcxproj 项目使用 Visual Studio 项目系统的扩展性[部署提供程序](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDeployProvider.md)。

### <a name="build-up-to-date-check"></a>生成最新检查

默认情况下，生成最新检查需要读取的.tlog 和写入.tlog 文件要在其中创建`$(TlogLocation)`所有生成输入和输出的生成过程的文件夹。

若要使用自定义的最新检查：

1. 通过添加禁用默认的最新检查`NoVCDefaultBuildUpToDateCheckProvider`中的功能*Toolset.targets*文件：

   ```xml
   <ItemGroup>
     <ProjectCapability Include="NoVCDefaultBuildUpToDateCheckProvider" />
   </ItemGroup>
   ```

1. 实现您自己[IBuildUpToDateCheckProvider](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IBuildUpToDateCheckProvider.md)。

## <a name="project-upgrade"></a>项目升级

### <a name="default-vcxproj-project-upgrader"></a>默认.vcxproj 项目升级程序

默认.vcxproj 项目升级程序更改`PlatformToolset`， `ApplicationTypeRevision`，MSBuild 工具集版本和.Net framework。 最后两个始终更改为 Visual Studio 版本的默认值，但`PlatformToolset`和`ApplicationTypeRevision`可通过特殊的 MSBuild 属性控制。

升级程序使用这些条件来确定一个项目可以或不进行升级：

1. 定义项目`ApplicationType`和`ApplicationTypeRevision`，具有较高修订版本比当前的文件夹。

1. 该属性`_UpgradePlatformToolsetFor_<safe_toolset_name>`定义当前工具集，并且其值不等于当前的工具集。

   在这些属性名称，  *\<safe_toolset_name >* 表示工具集名称，其中包含所有非字母数字字符替换为下划线 ( **\_** )。

当一个项目可以进行升级时，它参与了*解决方案重定目标*。 有关详细信息，请参阅[IVsTrackProjectRetargeting2](/dotnet/api/microsoft.visualstudio.shell.interop.ivstrackprojectretargeting2)。

如果你想要修饰中的项目名称**解决方案资源管理器**时的项目使用特定的工具集，定义`_PlatformToolsetShortNameFor_<safe_toolset_name>`属性。

有关的示例`_UpgradePlatformToolsetFor_<safe_toolset_name>`并`_PlatformToolsetShortNameFor_<safe_toolset_name>`属性定义，请参阅*Microsoft.Cpp.Default.props*文件。 有关用法的示例，请参阅`$(VCTargetPath)` \\ *Microsoft.Cpp.Platform.targets*文件。

### <a name="custom-project-upgrader"></a>自定义项目升级程序

若要使用自定义项目升级程序对象，实现一个 MEF 组件，如下所示：

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

你的代码可以导入和调用默认.vcxproj 升级程序对象：

```csharp
// ...
[Import("VCDefaultProjectUpgrader")]
// ...
    IProjectRetargetHandler Lazy<IProjectRetargetHandler>
    VCDefaultProjectUpgrader { get; set; }
// ...
```

`IProjectRetargetHandler` 在中定义*Microsoft.VisualStudio.ProjectSystem.VS.dll* ，它类似于`IVsRetargetProjectAsync`。

定义`VCProjectUpgraderObjectName`属性来告诉项目系统使用自定义 upgrader 对象：

```xml
<PropertyGroup>
  <VCProjectUpgraderObjectName>MyProjectUpgrader</VCProjectUpgraderObjectName>
</PropertyGroup>
```

#### <a name="disable-project-upgrade"></a>禁用项目升级

若要禁用项目的升级，请使用`NoUpgrade`值：

```xml
<PropertyGroup>
  <VCProjectUpgraderObjectName>NoUpgrade</VCProjectUpgraderObjectName>
</PropertyGroup>
```

## <a name="project-cache-and-extensibility"></a>项目缓存和可扩展性

若要使用较大时提高性能C++在 Visual Studio 2017 中，解决方案[项目缓存](https://devblogs.microsoft.com/cppblog/faster-c-solution-load-with-vs-15/)引入了。 它作为一个填充了项目数据，并随后用于加载项目，而不加载到内存中的 MSBuild 或 CPS 项目的 SQLite 数据库实现。

由于存在可用于从缓存加载的.vcxproj 项目没有 CPS 对象，该扩展的 MEF 组件的导入`UnconfiguredProject`或`ConfiguredProject`无法创建。 若要支持可扩展性，Visual Studio 会检测是否一个项目使用 （或可能使用） MEF 扩展时，不使用项目缓存。

这些项目类型始终是完全加载并且 CPS 对象在内存中，以便为其创建所有 MEF 扩展：

- 启动项目

- 它是具有自定义项目升级程序中，项目，他们会定义`VCProjectUpgraderObjectName`属性

- 不，它是针对桌面 Windows 的项目，他们会定义`ApplicationType`属性

- 通过在它们的.vcxitems 项目导入该引用的共享项项目 (.vcxitems) 和任何项目。

如果检测到以下任何情况，则创建的项目缓存。 缓存包含需要回答的 MSBuild 项目中的所有数据`get`查询上的`VCProjectEngine`接口。 这意味着在 MSBuild 属性的所有修改和扩展来完成的目标文件级别应该可以从缓存加载的项目中正常工作。

## <a name="shipping-your-extension"></a>传送你的扩展

有关如何创建 VSIX 文件的信息，请参阅[传送 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)。 有关如何将文件添加到特殊的安装位置，例如，若要添加下的文件的信息`$(VCTargetsPath)`，请参阅[扩展文件夹外安装](../extensibility/set-install-root.md)。

## <a name="additional-resources"></a>其他资源

Microsoft 生成系统 ([MSBuild](../msbuild/msbuild.md)) 为项目文件中提供的生成引擎和可扩展的基于 XML 的格式。 您应了解使用 basic [MSBuild 概念](../msbuild/msbuild-concepts.md)和如何[视觉对象的 MSBuild C++ ](/cpp/build/reference/msbuild-visual-cpp-overview)若要将视觉对象扩展的工作原理C++项目系统。

Managed Extensibility Framework ([MEF](/dotnet/framework/mef/)) 提供了扩展 CPS 和视觉对象所使用的 ApiC++项目系统。 CPS 如何使用 MEF 的概述，请参阅[CPS，MEF](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/mef.md#cps-and-mef)中[VSProjectSystem 概述 MEF](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/mef.md)。

您可以自定义现有的生成系统，以添加生成步骤或新的文件类型。 有关详细信息，请参阅[MSBuild (Visual C++) 概述](/cpp/build/reference/msbuild-visual-cpp-overview)并[使用项目属性](/cpp/build/working-with-project-properties)。
