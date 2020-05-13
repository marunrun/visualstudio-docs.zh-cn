---
title: MSBuild 命令行参考 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, msbuild.exe
- MSBuild, command line reference
- msbuild.exe
ms.assetid: edaa65ec-ab8a-42a1-84cb-d76d5b2f4584
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 90354cdc30785099d68d36781d7916de52b58705
ms.sourcegitcommit: 0b8497b720eb06bed8ce2194731177161b65eb84
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82072354"
---
# <a name="msbuild-command-line-reference"></a>MSBuild 命令行参考

使用 MSBuild.exe 生成项目或解决方案文件时，可以包含几个开关来指定过程的各个方面  。

每个开关都有两种形式：-switch 和 /switch。 本文档仅介绍 -switch 形式。 开关不区分大小写。 如果从 Windows 命令提示符之外的 shell 运行 MSBuild，则开关的参数列表（用分号或逗号分隔）可能需要单引号或双引号，以确保将列表传递到 MSBuild，而不是由 shell 解释。

## <a name="syntax"></a>语法

```cmd
MSBuild.exe [Switches] [ProjectFile]
```

## <a name="arguments"></a>自变量

|参数|描述|
|--------------|-----------------|
|`ProjectFile`|在指定项目文件中生成目标。 如果不指定项目文件，则 MSBuild 会在当前工作目录中搜索以“proj”结尾的文件扩展名并使用该文件  。 还可以为此参数指定 Visual Studio 解决方案文件。|

## <a name="switches"></a>开关

|开关|缩写形式|描述|
|------------|----------------|-----------------|
|-detailedSummary|-ds|在生成日志末尾显示有关生成的配置以及如何将它们安排到节点中的详细信息。|
|-graphBuild[:`True` or `False`]|-graph[:`True` or `False`]|使 MSBuild 构造和生成项目图。 构图涉及标识对窗体依赖项的项目引用。 生成该图涉及到尝试在引用它们的项目之前生成项目引用，这不同于传统的 MSBuild 计划。|
|-help|/? 或 -h|显示用法信息。 以下命令是一个示例：<br /><br /> `msbuild.exe -?`|
|-ignoreProjectExtensions: `extensions`|-ignore: `extensions`|确定要生成的项目文件时忽略指定扩展名。 使用分号或逗号分隔多个扩展名，如以下示例所示：<br /><br /> `-ignoreprojectextensions:.vcproj,.sln`|
|-interactive[:`True` or `False`]|-|指示允许生成中的操作与用户交互。  不要在不期望交互的自动方案中使用此参数。 指定 -interactive 等效于指定 -interactive:true。  使用此参数重写来自响应文件的值。
|-isolateProjects[:`True` or `False`]|-isolate[:`True` or `False`]|使 MSBuild 单独生成每个项目。 这是 MSBuild 更严格的模式，因为它要求在计算时可以静态发现项目图，但生成大量项目时可以改进计划并减少内存开销。|
|-maxCpuCount[:`number`]|-m[:`number`]|指定生成时要使用的最大并发进程数。 如果不包含此开关，则默认值为 1。 如果包含此开关而没有指定值，MSBuild 将使用计算机中的处理器总数作为其值。 有关详细信息，请参阅[并行生成多个项目](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)。<br /><br /> 下面的示例指示 MSBuild 使用三个 MSBuild 进程进行生成，这允许同时生成三个项目：<br /><br /> `msbuild myproject.proj -maxcpucount:3`|
|-noAutoResponse|-noautorsp|不自动包含任何 MSBuild.rsp 文件  。|
|-nodeReuse:`value`|-nr:`value`|启用或禁用 MSBuild 节点的重复使用。 你可以指定以下值：<br /><br /> -   **True**。 节点在生成完成之后保留，以便后续生成可以使用它们（默认值）。<br />-   **False**。 节点在生成完成之后不保留。<br /><br /> 节点对应于正在执行的项目。 如果你添加 -maxcpucount  开关，多个节点可并发执行。|
|-nologo||不显示启动版权标志或版权消息。|
|<a name="preprocess"></a> -preprocess[:`filepath`]|-pp[:`filepath`]|通过内联会在生成期间导入的所有文件（标记其边界）创建单一的聚合项目文件。 可以使用此开关更轻松地确定所导入的文件、从中导入文件的位置以及参与生成的文件。 使用此开关时，不生成项目。<br /><br /> 如果指定 `filepath`，则会将聚合项目文件输出到文件。 否则，输出将显示在控制台窗口中。<br /><br /> 有关如何使用 `Import` 元素将项目文件插入到其他项目文件的详细信息，请参阅 [Import 元素 (MSBuild)](../msbuild/import-element-msbuild.md) 和[如何：在多个项目文件中使用同一目标](../msbuild/how-to-use-the-same-target-in-multiple-project-files.md)。|
|-outputResultsCache[:cacheFile]|-orc[:cacheFile]|MSBuild 将在生成结束时将生成结果缓存的内容写入 Output 缓存文件。 设置此项还会打开独立生成 (-isolate)。|
|-profileEvaluation:`<file>`|-|分析 MSBuild 计算，并将结果写入指定的文件。 如果指定的文件的扩展名为“.md”，则以 Markdown 格式生成结果。 否则，将生成制表符分隔文件。|
|-property:`name`=`value`|-p:`name`=`value`|设置或重写指定项目级属性，其中 `name` 是属性名称，`value` 是属性值。 单独指定每个属性，或使用分号或逗号分隔多个属性，如以下示例所示：<br /><br /> `-property:WarningLevel=2;OutDir=bin\Debug`|
|-restore|-r|在生成实际目标之前运行 `Restore` 目标。|
|-restoreProperty:`name=value`|-rp:`name=value`|仅在还原期间设置或重写这些项目级别的属性，不要使用通过 -property 参数指定的属性。 `name` 是属性名称，`value` 是属性值。 使用分号或逗号分隔多个属性，或单独指定每个属性。|
|-target:`targets`|-t:`targets`|在项目中生成指定目标。 单独指定每个目标，或使用分号或逗号分隔多个目标，如以下示例所示：<br /><br /> `-target:PrepareResources;Compile`<br /><br /> 如果使用此开关指定任何目标，则它们会代替项目文件中的 `DefaultTargets` 特性中的任何目标来运行。 有关详细信息，请参阅[目标生成顺序](../msbuild/target-build-order.md)和[如何：指定首先生成的目标](../msbuild/how-to-specify-which-target-to-build-first.md)。<br /><br /> 目标是一组任务。 有关详细信息，请参阅[目标](../msbuild/msbuild-targets.md)。|
|-toolsVersion:`version`|-tv:`version`|指定要用于生成项目的工具集的版本，如以下示例所示：`-toolsversion:3.5`<br /><br /> 使用此开关可以生成项目并指定与 [Project 元素 (MSBuild)](../msbuild/project-element-msbuild.md) 中指定的版本不同的版本。 有关详细信息，请参阅[重写 ToolsVersion 设置](../msbuild/overriding-toolsversion-settings.md)。<br /><br /> 对于 MSBuild 4.5，可以为 `version` 指定以下值：2.0、3.5 和 4.0。 如果指定 4.0，`VisualStudioVersion` 生成属性会指定要使用的子工具集。 有关详细信息，请参阅[工具集 (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md) 的“子工具集”一节。<br /><br /> 包含用于生成应用程序的任务、目标和工具的工具集。 工具包括编译器，例如 csc.exe 和 vbc.exe   。 有关工具集的详细信息，请参阅[工具集 (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)、[标准和自定义工具集配置](../msbuild/standard-and-custom-toolset-configurations.md)和[多定向](../msbuild/msbuild-multitargeting-overview.md)。 **注意：** 工具集版本与目标框架不同，后者是生成项目以在其上运行的 .NET Framework 的版本。 有关详细信息，请参阅[目标框架和目标平台](../msbuild/msbuild-target-framework-and-target-platform.md)。|
|-validate:[`schema`]|-val[`schema`]|验证项目文件，如果验证成功，则生成项目。<br /><br /> 如果没有指定 `schema`，则针对默认架构验证项目。<br /><br /> 如果指定 `schema`，则针对指定的架构验证项目。<br /><br /> 下面的设置是一个示例：`-validate:MyExtendedBuildSchema.xsd`|
|-verbosity:`level`|-v:`level`|指定要在生成日志中显示的信息量。 每个记录器基于为该记录器设置的详细级别显示事件。<br /><br /> 可以指定以下详细级别：`q[uiet]`、`m[inimal]`、`n[ormal]`（默认）、`d[etailed]` 和 `diag[nostic]`。<br /><br /> 下面的设置是一个示例：`-verbosity:quiet`
|-version|-ver|仅显示版本信息。 不生成项目。|
|@`file`||从文本文件插入命令行开关。 如果具有多个文件，可单独指定它们。 有关详细信息，请参阅[响应文件](../msbuild/msbuild-response-files.md)。|
|-warnAsError[:`code`[`;code2`]|-err[`:code`[`;code2`]|要视为错误的警告代码的列表。  使用分号或逗号分隔多个警告代码。 若要将所有警告视为错误，请使用不带任何值的开关。 如果警告被视为错误，则目标将像对待警告一样继续执行，但总体生成会失败。<br/><br/>示例：`-err:MSB4130`|
|-warnAsMessage[:`code`[`;code2`]|-noWarn[:`code`[`;code2`]|要视为低重要性消息的警告代码的列表。  使用分号或逗号分隔多个警告代码。<br/><br/>示例：`-noWarn:MSB3026`|

### <a name="switches-for-loggers"></a>记录器的开关

|开关|缩写形式|描述|
|------------|----------------|-----------------|
|-binaryLogger[:[LogFile=]`output.binlog`<br/>[;ProjectImports=[None,Embed,ZipFile]]]|-bl|将所有生成事件串行化为压缩的二进制文件。 默认情况下，该文件位于当前目录中，名称为 msbuild.binlog  。 二进制日志是对生成过程的详细描述，可在将来用于重建文本日志，或由其它分析工具使用。 二进制日志的大小通常只有最详细文本诊断级日志的 1/10 到 1/20，但却能包含更多信息。<br /><br />二进制记录器默认收集项目文件的源文本，包括所有导入的项目，以及在生成期间所遇到的目标文件。 可选的 `ProjectImports` 开关控制此行为：<br /><br /> -   ProjectImports=None  。 不收集项目导入。<br /> -   ProjectImports=Embed  。 在日志文件中嵌入项目导入（默认）。<br /> -   ProjectImports=ZipFile  。 将项目文件保存至 \<output>.projectimports.zip，其中 \<output> 的名称与二进制日志文件的名称相同  。<br /><br />ProjectImports 的默认设置为“嵌入”。<br />请注意：记录器不收集 .cs、.cpp 等非 MSBuild 源文件    。<br />将 .binlog 文件作为参数而非项目/解决方案传递给 msbuild.exe 可“播放”该文件   。 其他记录器将接收日志文件中包含的信息，就像原始生成发生时那样。 若要详细了解二进制日志及其使用情况，可访问 https://github.com/Microsoft/msbuild/wiki/Binary-Log <br /><br />示例： <br /> -   `-bl`<br /> -    `-bl:output.binlog`<br /> -   `-bl:output.binlog;ProjectImports=None`<br /> -   `-bl:output.binlog;ProjectImports=ZipFile`<br /> -   `-bl:..\..\custom.binlog`<br /> -   `-binaryLogger`|
|-consoleLoggerParameters:<br /><br /> `parameters`|-clp:`parameters`|将指定的参数传递到控制台记录器，后者会在控制台窗口中显示生成信息。 可以指定以下参数：<br /><br /> -   **PerformanceSummary**。 显示在任务、目标和项目中所花费的时间。<br />-   **Summary**。 在末尾显示错误和警告摘要。<br />-   **NoSummary**。 不在末尾显示错误和警告摘要。<br />-   **ErrorsOnly**。 仅显示错误。<br />-   **WarningsOnly**。 仅显示警告。<br />-   **NoItemAndPropertyList**。 如果详细级别设置为 `diagnostic`，则不在每个项目生成开头显示项和属性的列表。<br />-   **ShowCommandLine**。 显示 `TaskCommandLineEvent` 消息。<br />-   **ShowTimestamp**。 将时间戳显示为任何消息的前缀。<br />-   **ShowEventId**。 显示每个已启动事件、已完成事件和消息的事件 ID。<br />-   **ForceNoAlign**。 不将文本与控制台缓冲区大小对齐。<br />-   **DisableConsoleColor**。 将默认控制台颜色用于所有日志记录消息。<br />-   **DisableMPLogging**。 在非多处理器模式下运行时，禁用输出的多处理器日志记录样式。<br />-   **EnableMPLogging**。 启用多处理器日志记录样式（即使在非多处理器模式下运行）。 默认情况下，此日志记录样式处于启用状态。<br />-   **Verbosity**。 重写此记录器的 -verbosity  设置。<br /><br /> 使用分号分隔多个参数，如以下示例所示：<br /><br /> `-consoleloggerparameters:PerformanceSummary;NoSummary -verbosity:minimal`<br/><br/> 默认控制台记录器的详细级别为 normal，并包括 `Summary`。|
|-distributedFileLogger|-dfl|将每个 MSBuild 节点的生成输出记录到其自己的文件。 这些文件的初始位置是当前目录。 默认情况下，这些文件命名为“MSBuild\<NodeId>.log”  。 可使用 -fileLoggerParameters  开关指定文件位置和 fileLogger 的其他参数。<br /><br /> 如果你使用 -fileLoggerParameters  开关命名日志文件，分布式记录器会在为每个节点创建日志文件时，将相应名称用作模板，并将节点 ID 追加到相应名称中。|
|-distributedLogger:<br /><br /> `central logger`*<br /><br /> `forwarding logger`|-dl:`central logger`*`forwarding logger`|记录 MSBuild 中的事件，将不同记录器实例附加到每个节点。 若要指定多个记录器，请分别指定每个记录器。<br /><br /> 使用记录器语法指定记录器。 有关记录器语法，请参阅下面的 logger  开关。<br /><br /> 下面的示例演示如何使用此开关：<br /><br /> `-dl:XMLLogger,MyLogger,Version=1.0.2,Culture=neutral`<br /><br /> `-dl:MyLogger,C:\My.dll*ForwardingLogger,C:\Logger.dll`|
|-fileLogger<br /><br /> *[number]*|-fl[`number`]|将生成输出记录到当前目录中的单个文件。 如果没有指定 `number`，输出文件名为 msbuild.log  。 如果指定 `number`，输出文件名为 msbuild\<n>.log，其中 \<n> 是 `number` 。 `Number` 可以是 1 到 9 的数字。<br /><br /> 可使用 -fileLoggerParameters  开关指定文件位置和 fileLogger 的其他参数。|
|-fileLoggerParameters:[number]<br /><br /> `parameters`|-flp[ `number`]: `parameters`|为文件记录器和分布式文件记录器指定任何额外参数。 若有此开关，表明存在对应的 -filelogger[  `number`]  开关。 `Number` 可以是 1 到 9 的数字。<br /><br /> 可使用针对 -consoleloggerparameters  列出的所有参数。 还可以使用以下一个或多个参数：<br /><br /> -   **LogFile**。 写入生成日志的日志文件的路径。 分布式文件记录器将此路径用作其日志文件的名称的前缀。<br />-   **Append**。 确定是将生成日志追加到日志文件还是覆盖它。 设置该开关时，生成日志将追加到日志文件。 此开关不存在时，将覆盖现有日志文件的内容。<br />     如果包含追加开关，则无论它是设置为 true 还是 false，都会追加日志。 如果不包含追加开关，则会覆盖日志。<br />     在此例中会覆盖文件：`msbuild myfile.proj -l:FileLogger,Microsoft.Build;logfile=MyLog.log`<br />     在此例中会追加文件：`msbuild myfile.proj -l:FileLogger,Microsoft.Build;logfile=MyLog.log;append=true`<br />     在此例中会追加文件：`msbuild myfile.proj -l:FileLogger,Microsoft.Build;logfile=MyLog.log;append=false`<br />-   **Encoding**。 指定文件的编码（例如，UTF-8、Unicode 或 ASCII）。<br /><br /> 下面的示例为警告和错误生成单独的日志文件：<br /><br /> `-flp1:logfile=errors.txt;errorsonly -flp2:logfile=warnings.txt;warningsonly`<br /><br /> 下面的示例演示其他可能性：<br /><br /> `-fileLoggerParameters:LogFile=MyLog.log;Append; Verbosity=diagnostic;Encoding=UTF-8`<br /><br /> `-flp:Summary;Verbosity=minimal;LogFile=msbuild.sum`<br /><br /> `-flp1:warningsonly;logfile=msbuild.wrn`<br /><br /> `-flp2:errorsonly;logfile=msbuild.err`|
|-logger:<br /><br /> `logger`|-l:`logger`|指定要用于记录 MSBuild 中的事件的记录器。 若要指定多个记录器，请分别指定每个记录器。<br /><br /> 将以下语法用于 `logger`: `[``LoggerClass``,]``LoggerAssembly``[;``LoggerParameters``]`<br /><br /> 将以下语法用于 `LoggerClass`: `[``PartialOrFullNamespace``.]``LoggerClassName`<br /><br /> 如果程序集恰好包含一个记录器，则不必指定记录器类。<br /><br /> 将以下语法用于 `LoggerAssembly`：`{``AssemblyName``[,``StrongName``] &#124;` `AssemblyFile``}`<br /><br /> 记录器参数是可选的，传递给记录器时与输入时完全一致。<br /><br /> 下面的示例使用 -logger  开关。<br /><br /> `-logger:XMLLogger,MyLogger,Version=1.0.2,Culture=neutral`<br /><br /> `-logger:XMLLogger,C:\Loggers\MyLogger.dll;OutputAsHTML`|
|-noConsoleLogger|-noconlog|禁用默认控制台记录器，不将事件记录到控制台。|

## <a name="example"></a>示例

 下面的示例生成 MyProject.proj 项目的 `rebuild` 目标  。

```cmd
MSBuild.exe MyProject.proj -t:rebuild
```

## <a name="example"></a>示例

 可以使用 MSBuild.exe 执行更复杂的生成  。 例如，可以使用它在解决方案中生成特定项目的特定目标。 下面的示例重新生成项目 `NotInSolutionFolder` 并清理项目 `InSolutionFolder`（位于 NewFolder 解决方案文件夹中）  。

```cmd
msbuild SlnFolders.sln -t:NotInSolutionfolder:Rebuild;NewFolder\InSolutionFolder:Clean
```

## <a name="see-also"></a>请参阅

- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [常用的 MSBuild 项目属性](../msbuild/common-msbuild-project-properties.md)
