---
title: MSBuild 命令行参考 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
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
caps.latest.revision: 61
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8d40bfefb1f89496b538612dfa1819cc6d65c76c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68181054"
---
# <a name="msbuild-command-line-reference"></a>MSBuild 命令行参考
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 MSBuild.exe 生成项目或解决方案文件时，可以包含几个开关来指定过程的各个方面。  
  
## <a name="syntax"></a>语法  
  
```  
MSBuild.exe [Switches] [ProjectFile]  
```  
  
## <a name="arguments"></a>参数  
  
|参数|描述|  
|--------------|-----------------|  
|`ProjectFile`|在指定项目文件中生成目标。 如果不指定项目文件，则 MSBuild 会在当前工作目录中搜索以“proj”结尾的文件扩展名并使用该文件。 还可以为此参数指定 Visual Studio 解决方案文件。|  
  
## <a name="switches"></a>开关  
  
|开关|缩写形式|描述|  
|------------|----------------|-----------------|  
|/help|/? 或 /h|显示用法信息。 以下命令是一个示例：<br /><br /> `msbuild.exe /?`|  
|/detailedsummary|/ds|在生成日志末尾显示有关生成的配置以及如何将它们安排到节点中的详细信息。|  
|/ignoreprojectextensions: `extensions`|/ignore: `extensions`|确定要生成的项目文件时忽略指定扩展名。 使用分号或逗号分隔多个扩展名，如以下示例所示：<br /><br /> `/ignoreprojectextensions:.vcproj,.sln`|  
|/maxcpucount[:`number`]|/m[:`number`]|指定生成时要使用的最大并发进程数。 如果不包含此开关，则默认值为 1。 如果包含此开关而没有指定值，MSBuild 将使用计算机中的处理器总数作为其值。 有关详细信息，请参阅[并行生成多个项目](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)。<br /><br /> 下面的示例指示 MSBuild 使用三个 MSBuild 进程进行生成，这允许同时生成三个项目：<br /><br /> `msbuild myproject.proj /maxcpucount:3`|  
|/noautoresponse|/noautorsp|不自动包含任何 MSBuild.rsp 文件。|  
|/nodeReuse:`value`|/nr:`value`|启用或禁用 MSBuild 节点的重复使用。 你可以指定以下值：<br /><br /> -   **True**。 节点在生成完成之后保留，以便后续生成可以使用它们（默认值）。<br />-   **False**。 节点在生成完成之后不保留。<br /><br /> 节点对应于正在执行的项目。 如果包含 **/maxcpucount** 开关，则多个节点可以并发执行。|  
|/nologo||不显示启动版权标志或版权消息。|  
|/preprocess[:`filepath`]|/pp[:`filepath`]|通过内联会在生成期间导入的所有文件（标记其边界）创建单一的聚合项目文件。 可以使用此开关更轻松地确定所导入的文件、从中导入文件的位置以及参与生成的文件。 使用此开关时，不生成项目。<br /><br /> 如果指定 `filepath`，则会将聚合项目文件输出到文件。 否则，输出将显示在控制台窗口中。<br /><br /> 有关如何使用信息`Import`元素将项目文件插入到另一个项目文件，请参阅[Import 元素 (MSBuild)](../msbuild/import-element-msbuild.md)和[如何：在多个项目文件中使用同一目标](../msbuild/how-to-use-the-same-target-in-multiple-project-files.md)。|  
|/property:`name`=`value`|/p:`name`=`value`|设置或重写指定项目级属性，其中 `name` 是属性名称，`value` 是属性值。 单独指定每个属性，或使用分号或逗号分隔多个属性，如以下示例所示：<br /><br /> `/property:WarningLevel=2;OutDir=bin\Debug`|  
|/target:`targets`|/t:`targets`|在项目中生成指定目标。 单独指定每个目标，或使用分号或逗号分隔多个目标，如以下示例所示：<br /><br /> `/target:Resources;Compile`<br /><br /> 如果使用此开关指定任何目标，则它们会代替项目文件中的 `DefaultTargets` 特性中的任何目标来运行。 有关详细信息，请参阅[目标生成顺序](../msbuild/target-build-order.md)和[如何：指定首先生成的目标](../msbuild/how-to-specify-which-target-to-build-first.md)。<br /><br /> 目标是一组任务。 有关详细信息，请参阅[目标](../msbuild/msbuild-targets.md)。|  
|/toolsversion:`version`|/tv:`version`|指定要用于生成项目的工具集的版本，如以下示例所示：`/toolsversion:3.5`<br /><br /> 使用此开关可以生成项目并指定与 [Project 元素 (MSBuild)](../msbuild/project-element-msbuild.md) 中指定的版本不同的版本。 有关详细信息，请参阅[重写 ToolsVersion 设置](../msbuild/overriding-toolsversion-settings.md)。<br /><br /> 对于 MSBuild 4.5，可以为 `version` 指定以下值：2.0、3.5 和 4.0。 如果指定 4.0，`VisualStudioVersion` 生成属性会指定要使用的子工具集。 有关详细信息，请参阅[工具集 (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md) 的“子工具集”一节。<br /><br /> 包含用于生成应用程序的任务、目标和工具的工具集。 工具包括编译器例如 csc.exe 和 vbc.exe。 有关工具集的详细信息，请参阅[工具集 (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)、[标准和自定义工具集配置](../msbuild/standard-and-custom-toolset-configurations.md)和[多定向](../msbuild/msbuild-multitargeting-overview.md)。 **注意：** 工具集版本与目标框架不同，后者是生成项目以其其上运行的 .NET Framework 的版本。 有关详细信息，请参阅[目标框架和目标平台](../msbuild/msbuild-target-framework-and-target-platform.md)。|  
|/validate:[`schema`]|/val[`schema`]|验证项目文件，如果验证成功，则生成项目。<br /><br /> 如果没有指定 `schema`，则针对默认架构验证项目。<br /><br /> 如果指定 `schema`，则针对指定的架构验证项目。<br /><br /> 下面的设置是一个示例：`/validate:MyExtendedBuildSchema.xsd`|  
|/verbosity:`level`|/v:`level`|指定要在生成日志中显示的信息量。 每个记录器基于为该记录器设置的详细级别显示事件。<br /><br /> 可以指定以下详细级别：`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。<br /><br /> 下面的设置是一个示例：`/verbosity:quiet`|  
|/version|/ver|仅显示版本信息。 不生成项目。|  
|@`file`||从文本文件插入命令行开关。 如果具有多个文件，可单独指定它们。 有关详细信息，请参阅[响应文件](../msbuild/msbuild-response-files.md)。|  
  
### <a name="switches-for-loggers"></a>记录器的开关  
  
|开关|缩写形式|描述|  
|------------|----------------|-----------------|  
|/consoleloggerparameters:<br /><br /> `parameters`|/clp:`parameters`|将指定的参数传递到控制台记录器，后者会在控制台窗口中显示生成信息。 可以指定以下参数：<br /><br /> -   **PerformanceSummary**。 显示在任务、目标和项目中所花费的时间。<br />-   **Summary**。 在末尾显示错误和警告摘要。<br />-   **NoSummary**。 不在末尾显示错误和警告摘要。<br />-   **ErrorsOnly**。 仅显示错误。<br />-   **WarningsOnly**。 仅显示警告。<br />-   **NoItemAndPropertyList**。 如果详细级别设置为 `diagnostic`，则不在每个项目生成开头显示项和属性的列表。<br />-   **ShowCommandLine**。 显示 `TaskCommandLineEvent` 消息。<br />-   **ShowTimestamp**。 将时间戳显示为任何消息的前缀。<br />-   **ShowEventId**。 显示每个已启动事件、已完成事件和消息的事件 ID。<br />-   **ForceNoAlign**。 不将文本与控制台缓冲区大小对齐。<br />-   **DisableConsoleColor**。 将默认控制台颜色用于所有日志记录消息。<br />-   **DisableMPLogging**。 在非多处理器模式下运行时，禁用输出的多处理器日志记录样式。<br />-   **EnableMPLogging**。 启用多处理器日志记录样式（即使在非多处理器模式下运行）。 默认情况下，此日志记录样式处于启用状态。<br />-   **Verbosity**。 重写此记录器的 **/verbosity** 设置。<br /><br /> 使用分号或逗号分隔多个参数，如以下示例所示：<br /><br /> `/consoleloggerparameters:PerformanceSummary;NoSummary /verbosity:minimal`|  
|/distributedFileLogger|/dfl|将每个 MSBuild 节点的生成输出记录到其自己的文件。 这些文件的初始位置是当前目录。 默认情况下，这些文件命名为“MSBuild*NodeId*.log”。 可以使用 **/fileLoggerParameters** 开关指定文件位置和 fileLogger 的其他参数。<br /><br /> 如果使用 **/fileLoggerParameters** 开关命名日志文件，则分布式记录器会在为每个节点创建日志文件时使用该名称作为模板并将节点 ID 追加到该名称。|  
|/distributedlogger:<br /><br /> `central logger`*<br /><br /> `forwarding logger`|/dl:`central logger`*`forwarding logger`|记录 MSBuild 中的事件，将不同记录器实例附加到每个节点。 若要指定多个记录器，请分别指定每个记录器。<br /><br /> 使用记录器语法指定记录器。 有关记录器语法，请参阅下面的 **/logger** 开关。<br /><br /> 下面的示例演示如何使用此开关：<br /><br /> `/dl:XMLLogger,MyLogger,Version=1.0.2,Culture=neutral`<br /><br /> `/dl:MyLogger,C:\My.dll*ForwardingLogger,C:\Logger.dll`|  
|/fileLogger<br /><br /> *[number]*|/fl[`number`]|将生成输出记录到当前目录中的单个文件。 如果没有指定 `number`，输出文件名为 msbuild.log。 如果指定 `number`，输出文件名为 msbuild`n`.log，其中 n 是 `number`。 `Number` 可以是 1 到 9 的数字。<br /><br /> 可以使用 **/fileLoggerParameters** 开关指定文件位置和 fileLogger 的其他参数。|  
|/fileloggerparameters:[number]<br /><br /> `parameters`|/flp:[ `number`] `parameters`|为文件记录器和分布式文件记录器指定任何额外参数。 此开关的存在意味着存在对应的 /**filelogger[** `number` **]** 开关。 `Number` 可以是 1 到 9 的数字。<br /><br /> 可以使用为 **/consoleloggerparameters** 列出的所有参数。 还可以使用以下一个或多个参数：<br /><br /> -   **LogFile**。 写入生成日志的日志文件的路径。 分布式文件记录器将此路径用作其日志文件的名称的前缀。<br />-   **Append**。 确定是将生成日志追加到日志文件还是覆盖它。 设置该开关时，生成日志将追加到日志文件。 此开关不存在时，将覆盖现有日志文件的内容。<br />     如果包含追加开关，则无论它是设置为 true 还是 false，都会追加日志。 如果不包含追加开关，则会覆盖日志。<br />     在此例中会覆盖文件：`msbuild myfile.proj /l:FileLogger,Microsoft.Build.Engine;logfile=MyLog.log`<br />     在此例中会追加文件：`msbuild myfile.proj /l:FileLogger,Microsoft.Build.Engine;logfile=MyLog.log;append=true`<br />     在此例中会追加文件：`msbuild myfile.proj /l:FileLogger,Microsoft.Build.Engine;logfile=MyLog.log;append=false`<br />-   **Encoding**。 指定文件的编码（例如，UTF-8、Unicode 或 ASCII）。<br /><br /> 下面的示例为警告和错误生成单独的日志文件：<br /><br /> `/flp1:logfile=errors.txt;errorsonly /flp2:logfile=warnings.txt;warningsonly`<br /><br /> 下面的示例演示其他可能性：<br /><br /> `/fileLoggerParameters:LogFile=MyLog.log;Append; Verbosity=diagnostic;Encoding=UTF-8`<br /><br /> `/flp:Summary;Verbosity=minimal;LogFile=msbuild.sum`<br /><br /> `/flp1:warningsonly;logfile=msbuild.wrn`<br /><br /> `/flp2:errorsonly;logfile=msbuild.err`|  
|/logger:<br /><br /> `logger`|/l:`logger`|指定要用于记录 MSBuild 中的事件的记录器。 若要指定多个记录器，请分别指定每个记录器。<br /><br /> 将以下语法用于 `logger`: `[``LoggerClass``,]``LoggerAssembly``[;``LoggerParameters``]`<br /><br /> 将以下语法用于 `LoggerClass`: `[``PartialOrFullNamespace``.]``LoggerClassName`<br /><br /> 如果程序集恰好包含一个记录器，则不必指定记录器类。<br /><br /> 将以下语法用于 `LoggerAssembly`: `{``AssemblyName``[,``StrongName``] &#124;` `AssemblyFile``}`<br /><br /> 记录器参数是可选的，传递给记录器时与输入时完全一致。<br /><br /> 下面的示例使用 **/logger** 开关。<br /><br /> `/logger:XMLLogger,MyLogger,Version=1.0.2,Culture=neutral`<br /><br /> `/logger:XMLLogger,C:\Loggers\MyLogger.dll;OutputAsHTML`|  
|/noconsolelogger|/noconlog|禁用默认控制台记录器，不将事件记录到控制台。|  
  
## <a name="example"></a>示例  
 下面的示例生成 `rebuild` 项目的 `MyProject.proj` 目标。  
  
```  
MSBuild.exe MyProject.proj /t:rebuild  
```  
  
## <a name="example"></a>示例  
 可以使用 MSBuild.exe 执行更复杂的生成。 例如，可以使用它在解决方案中生成特定项目的特定目标。 下面的示例重新生成项目 `NotInSolutionFolder` 并清理项目 `InSolutionFolder`（位于 `NewFolder` 解决方案文件夹中）。  
  
```  
msbuild SlnFolders.sln /t:NotInSolutionfolder:Rebuild;NewFolder\InSolutionFolder:Clean  
```  
  
## <a name="see-also"></a>请参阅  
 [MSBuild 参考](../msbuild/msbuild-reference.md)   
 [常用的 MSBuild 项目属性](../msbuild/common-msbuild-project-properties.md)
