---
title: VSPerfReport | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- command-line tools, VSPerfReporttool
- performance tools, VSPerfReport tool
- profiling tools,VSPerfReport
- VSPerfReport tool
- command line, tools
- instrumentation, VSPerfReporttool
ms.assetid: dbfd8d91-4430-4b82-81b9-97ac61412a6c
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 54d5de2395c0ce95bc0c20c3ae7810b2762122fa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85329955"
---
# <a name="vsperfreport"></a>VSPerfReport
VSPerfReport 命令行工具可用于创建报表，这些报表使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具分析数据文件。 默认的报表格式为 .csv 文件  。

 VSPerfReport 使用以下语法：

```cmd
VSPerfReport [/U] vspfilename [/options]
```

 请注意，`filename` 必须是有效的.vsp 或 .vsps 文件   。

 VSPerfReport 命令行工具也可用于比较 .vsp 或 .vsps 文件   。 若要生成不同的 ("diff") 报表，请使用以下语法：

```cmd
VSPerfReport [/U] /diff vspfilename1 vspfilename2 [/options]
```

 `vspfilename1 and vspfilename2` 必须是有效的 .vsp 或.vsps 文件   。

## <a name="symbol-files"></a>符号文件
 为了显示函数名称和行号等符号信息，VSPerfReport 要求访问被分析组件的符号 (.PDB) 文件以及 Windows 符号文件。 有关详细信息，请参阅[如何：通过命令行指定符号文件位置](../profiling/how-to-specify-symbol-file-locations-from-the-command-line.md)。

## <a name="general-report-options"></a>常规报告选项
 下表说明了常规报表格式设置选项和用于选择要报告的数据的选项。

|选项|描述|
|-------------|-----------------|
|**U**|报表输出和重定向控制台输出是以 Unicode 形式写入的。 必须是指定的第一个选项。|
|**Summary:** [*types*]|创建一个或多个类型的报表。<br /><br /> -   `All` - 生成所有报表类型。<br />-   `CallerCallee` - 函数间的父/子关系。<br />-   `Function` - 调用的函数。<br />-   `CallTree` - 所调用函数的层次结构。<br />-   `Counter` - 所有标记，以及 Windows 性能计数器值。<br />-   `Ip` - 分析的说明。<br />-   `Life` - 已分配对象的生存期（在收集分配数据后可用）。<br />-   `Line` 源代码行配置文件数据。<br />-   `Header` - 报表包含文件头信息。<br />-   `Mark` 所有标记。<br />-   `Module` - 分析的模块。<br />-   `Process` - 分析的进程。<br />-   `Thread` - 分析的线程。<br />-   `Type` - 分配的类型。<br />-   `Contention` - 资源争用。<br />-   `RuleWarnings` - 性能规则问题<br />-   `ETW` - 运行分析期间收集的所有 Windows 事件跟踪 (ETW) 事件。 .etl 数据文件必须位于其原始位置，或位于包含 .vsp 或 .vsps 文件的目录中。|
|**Xml**|XML 格式的输出报表。|
|**CallTrace**|创建函数入口和出口、ETW 事件以及标记的列表。|
|**ClearPackedSymbols**|从探查器数据文件中删除先前嵌入的符号。 在第二次运行 PackSymbol 之前运行此命令。|
|**SymbolPath:** `path`|指定一个或多个搜索路径，或包含探查器数据文件符号的符号服务器。|
|**DebugSymPath**|列出在其中搜索符号的位置，并说明是否找到它们。 此选项有助于解决符号解析问题。|
|**PackSymbols**|将符号保存到分析数据 (.vsp) 文件，这样使得无需符号 (.pdb) 文件便可进行分析  。|
|**Output:** *path*&#124;*filename*|为生成的报表文件指定备用位置。 默认情况下，会在当前目录中创建报表。|
|**SummaryFile**|分析并将分析的信息保存在 .vsps 摘要文件中。|
|**PrintMarks**|显示指定报表文件中所有标记的名称和时间戳。|
|**?**|显示使用情况信息。|
|**NoLogo**|运行报表时隐藏版本信息。|
|**UserRulesDirectory**|指定包含用户定义的性能规则的目录 [尚未实现]。|

## <a name="filter-options"></a>筛选器选项
 下表说明了用于筛选可用数据的选项。

|选项|描述|
|-------------|-----------------|
|**JustMyCode**[ **:** [`caller`][,`callee`]]|仅显示用户应用程序函数调用；隐藏系统调用。<br /><br /> - 无参数 - 隐藏所有系统函数。<br />-   `caller` - 显示调用应用程序函数的系统函数的一个级别。<br />-   `callee` - 显示由用户应用程序函数调用的系统函数的一个级别。|
|**StartTime:** [*value*]|仅显示此值（以毫秒为单位）之后收集的数据。|
|**EndTime:** [*value*]|仅显示此值（以毫秒为单位）之前收集的数据。|
|**FilterFile:** `VSPFFile`|指定由 Visual Studio 性能报告窗口生成的筛选器文件的位置。|
|**MsFilter:** [*starttime,duration*]|仅显示从 `starttime` 到 `duration` 之间的数据（以毫秒为单位）。|
|**Process:** [*pid*]|仅显示来自指定进程的数据。|
|**Thread:** [*threadid*]|仅显示来自指定线程的数据。|
|**Thread:** [*threadid,processid*]|仅显示与指定进程相关联的指定线程的数据。|

## <a name="difference-report-options"></a>差异报告选项
 下表说明用于比较报表文件的选项。

|选项|描述|
|-------------|-----------------|
|**Diff**  `vspfile1 vspfile2`|比较两个报表文件（.vsp 或 .vsps）文件   。 使用 diff 选项将忽略摘要选项。|
|**Diff:** [*value*]|低于此阈值时，两个值之间的差异将被忽略。 此外，具有低于此阈值的值的数据将不会显示。|
|**DiffTable:** [*tablename*]|使用此特定表来比较文件。 默认为函数表。|
|**DiffColumn:** [*columnname*]|使用此特定列来比较值。 默认为独占样本百分比列。|
|**QueryDiffTables**|为提供的两个报表文件列出有效表和列。|

## <a name="see-also"></a>请参阅
- [性能报告视图](../profiling/performance-report-views.md)
