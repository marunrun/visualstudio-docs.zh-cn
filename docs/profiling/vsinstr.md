---
title: VSInstr | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- performance tools, instrumentation
- instrumentation, VSInstr tool
- profiling tools,VSInstr
- command-line tools, instrumentation
- command line, tools
- VSInstr
- VSInstr tool
- performance tools, VSInstr tool
ms.assetid: 7b1334f7-f9b0-4a82-a145-d0607bfa8467
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8af9195c0e9b36f804e16bd8903cfcfcd094032d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62822854"
---
# <a name="vsinstr"></a>VSInstr
VSInstr 工具用于检测二进制文件。 使用以下语法调用该工具：

```cmd
VSInstr [/U] filename [/options]
```

 下表描述了 VSInstr 工具选项：

|选项|说明|
|-------------|-----------------|
|**Help** 或 **?**|显示帮助。|
|**U**|以 Unicode 形式写入重定向的控制台输出。 它必须是指定的第一个选项。|
|`@filename`|指定响应文件的名称，其中每行包含一个命令选项。  不要使用引号。|
|**OutputPath** `:path`|指定被检测映像的目标目录。 如果未指定输出路径，则通过在同一目录中向文件名追加“Orig”对原始的二进制文件进行重命名，并且会检测到二进制文件的副本。|
|**Exclude** `:funcspec`|指定要由探测从检测中排除的函数规范。 当函数中的分析探测插入造成不可预测或不需要的结果时，它将十分有用。<br /><br /> 不要使用引用同一目录中的函数的“Exclude”和“Include”选项。<br /><br /> 可使用单独的“Exclude”选项指定多个函数规范。<br /><br /> `funcspec` 被定义为：<br /><br /> [namespace\<separator1>] [class\<separator2>]function<br /><br /> 对于本机代码，\<separator1> 是 `::`，对于托管代码，则是 `.`。<br /><br /> \<separator2> 始终为 `::`<br /><br /> 代码覆盖率支持 **Exclude**。<br /><br /> 支持通配符 \*。 例如，若要排除命名空间中的所有函数，请使用：<br /><br /> MyNamespace::\*<br /><br /> 可以使用 **VSInstr /DumpFuncs** 列出指定二进制文件中的函数的完整名称。|
|**Include** `:funcspec`|指定二进制文件中的函数规范以使用探测进行检测。 未检测二进制文件中的所有其他函数。<br /><br /> 可使用单独的“Include”选项指定多个函数规范。<br /><br /> 请不要使用引用同一目录中的函数的“Include”和“Exclude”选项。<br /><br /> 代码覆盖率不支持 **Include**。<br /><br /> `funcspec` 被定义为：<br /><br /> [namespace\<separator1>] [class\<separator2>]function<br /><br /> 对于本机代码，\<separator1> 是 `::`，对于托管代码，则是 `.`。<br /><br /> \<separator2> 始终为 `::`<br /><br /> 支持通配符 \*。 例如，若要包括命名空间中的所有函数，请使用：<br /><br /> MyNamespace::\*<br /><br /> 可以使用 **VSInstr /DumpFuncs** 列出指定二进制文件中的函数的完整名称。|
|**DumpFuncs**|列出指定映像中的函数。 未执行任何检测。|
|**ExcludeSmallFuncs**|从检测中排除较小的函数，它们是不执行任何函数调用的短函数。 “ExcludeSmallFuncs”选项提供了更少的检测开销，因此提高了检测速度。<br /><br /> 排除较小的函数也可减少进行分析所需的 .vsp 文件的大小和时间。|
|**Mark:**{**Before**`&#124;`**After**`&#124;`**Top**`&#124;`**Bottom**}`,funcname,markid`|插入可用于标识 .vsp 报表文件中数据区域的开始或结束处的分析标记（用于分隔报表中的数据的标识符）。<br /><br /> **Before** - 紧邻在目标函数进入前。<br /><br /> **After** - 紧邻目标函数退出后。<br /><br /> **Top** - 紧邻目标函数进入后。<br /><br /> **Bottom** - 紧邻目标函数中的每个返回值前。<br /><br /> `funcname` - 目标函数的名称<br /><br /> `Markid` - 用作分析标记的标识符的正整数（长整型）。|
|**Coverage**|执行覆盖率检测。 它只能用于以下选项：“Verbose”、“OutputPath”、“Exclude”和“Logfile”。|
|**Verbose**|“Verbose”选项用于查看检测进程的相关详细信息。|
|**NoWarn** `[:[Message Number[;Message Number]]]`|取消所有或特定警告。<br /><br /> `Message Number` - 警告编号。 如果省略 `Message Number`，则会取消所有警告。<br /><br /> 有关详细信息，请参阅 [VSInstr 警告](../profiling/vsinstr-warnings.md)。|
|**Control** `:{` **Thread** `&#124;` **Process** `&#124;` **Global** `}`|指定以下 VSInstr 数据收集控制选项的分析级别：<br /><br /> **Start**<br /><br /> **StartOnly**<br /><br /> **Suspend**<br /><br /> **StopOnly**<br /><br /> **SuspendOnly**<br /><br /> **ResumeOnly**<br /><br /> **Thread** - 指定线程级别的数据集合控制功能。 仅为当前线程启动或停止分析。 其他线程的分析状态不会受到影响。 默认值为 thread。<br /><br /> **Process** - 指定进程级别的分析数据集合控制功能。 为当前进程中的所有线程启动或停止分析。 其他进程的分析状态不会受到影响。<br /><br /> **Global** - 指定全局级别（跨进程）的数据集合控制功能。<br /><br /> 如果未指定分析级别，则会出现错误。|
|**Start** `:{` **Inside** `&#124;` **Outside** `},funcname`|将数据收集的范围限制为该函数所调用的目标函数和子函数。<br /><br /> **Inside** - 紧邻在目标函数的入口后插入 StartProfile 函数。 紧邻在目标函数中的每次返回前插入 StopProfile 函数。<br /><br /> **Outside** - 紧邻在对目标函数的每次调用前插入 StopProfile 函数。 紧邻在对目标函数的每次调用后插入 StopProfile 函数。<br /><br /> `funcname` - 目标函数的名称。|
|**Suspend** `:{` **Inside** `&#124;` **Outside** `},funcname`|排除该函数所调用的目标函数和子函数的数据集合。<br /><br /> **Inside** - 紧邻在目标函数的入口后插入 SuspendProfile 函数。 紧邻在目标函数中的每次返回前插入 ResumeProfile 函数。<br /><br /> **Outside** - 紧邻在目标函数的入口前插入 SuspendProfile 函数。 从目标函数中退出后立即插入 ResumeProfile 函数。<br /><br /> `funcname` - 目标函数的名称。<br /><br /> 如果目标函数包含 StartProfile 函数，则会在其之前插入 SuspendProfile 函数。 如果目标函数包含 StopProfile 函数，则会在其之后插入 ResumeProfile 函数。|
|**StartOnly：**`{` **Before** `&#124;` **After** `&#124;` **Top** `&#124;` **Bottom** `},funcname`|在分析运行期间开始数据收集。 它将在指定位置处插入 StartProfile API 函数。<br /><br /> **Before** - 紧邻在目标函数进入前。<br /><br /> **After** - 紧邻目标函数退出后。<br /><br /> **Top** - 紧邻目标函数进入后。<br /><br /> **Bottom** - 紧邻目标函数中的每个返回值前。<br /><br /> `funcname` - 目标函数的名称。|
|**StopOnly:**{**Before**`&#124;`**After**`&#124;`**Top**`&#124;`**Bottom**}`,funcname`|在分析运行期间停止数据收集。 它将在指定位置处插入 StopProfile 函数。<br /><br /> **Before** - 紧邻在目标函数进入前。<br /><br /> **After** - 紧邻目标函数退出后。<br /><br /> **Top** - 紧邻目标函数进入后。<br /><br /> **Bottom** - 紧邻目标函数中的每个返回值前。<br /><br /> `funcname` - 目标函数的名称。|
|**SuspendOnly:**{**Before**`&#124;`**After**`&#124;`**Top**`&#124;`**Bottom**}`,funcname`|在分析运行期间停止数据收集。 它将在指定位置处插入 SuspendProfile API 函数。<br /><br /> **Before** - 紧邻在目标函数进入前。<br /><br /> **After** - 紧邻目标函数退出后。<br /><br /> **Top** - 紧邻目标函数进入后。<br /><br /> **Bottom** - 紧邻目标函数中的每个返回值前。<br /><br /> `funcname` - 目标函数的名称。<br /><br /> 如果目标函数包含 StartProfile 函数，则会在其之前插入 SuspendProfile 函数。|
|**ResumeOnly:**{**Before**`&#124;`**After**`&#124;`**Top**`&#124;`**Bottom**}`,funcname`|在分析运行期间开始或恢复数据收集。<br /><br /> 它通常用于在 **SuspendOnly** 选项已停止分析后开始分析。 它将在指定位置处插入 ResumeProfile API 函数。<br /><br /> **Before** - 紧邻在目标函数进入前。<br /><br /> **After** - 紧邻目标函数退出后。<br /><br /> **Top** - 紧邻目标函数进入后。<br /><br /> **Bottom** - 紧邻目标函数中的每个返回值前。<br /><br /> `funcname` - 目标函数的名称。<br /><br /> 如果目标函数包含 StopProfile 函数，则会在其之后插入 ResumeProfile 函数。|

## <a name="see-also"></a>请参阅
- [VSPerfMon](../profiling/vsperfmon.md)
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [VSPerfReport](../profiling/vsperfreport.md)
- [VSInstr 警告](../profiling/vsinstr-warnings.md)
- [性能报告视图](../profiling/performance-report-views.md)