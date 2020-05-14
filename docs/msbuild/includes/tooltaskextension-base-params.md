---
author: ghogen
ms.author: ghogen
ms.topic: include
ms.date: 4/23/2020
ms.openlocfilehash: 40108f56ee9d64688fc665fdef0e0ab731bddfff
ms.sourcegitcommit: 596f92fcc84e6f4494178863a66aed85afe0bb08
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82204533"
---
### <a name="tooltaskextension-parameters"></a>ToolTaskExtension 参数

此任务继承自 <xref:Microsoft.Build.Tasks.ToolTaskExtension> 类，该类继承自 <xref:Microsoft.Build.Utilities.ToolTask> 类，后者本身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 此继承链向从它们派生的任务添加了几个参数。

下表介绍基类的参数：

| 参数 | 描述 |
| - | - |
| <xref:Microsoft.Build.Utilities.ToolTask.EchoOff%2A> | 可选 `bool` 参数。<br /><br /> 设置为 `true` 时，此任务会将 /Q  传递到 cmd.exe  命令行，以便命令行不会复制到 stdout。 |
| <xref:Microsoft.Build.Utilities.ToolTask.EnvironmentVariables%2A> | 可选的 `String` 数组参数。<br /><br /> 环境变量对的数组（使用等号分隔）。 这些变量会传递到生成的可执行文件以及（有选择地重写）常规环境块。 |
| <xref:Microsoft.Build.Utilities.ToolTask.ExitCode%2A> | 可选 `Int32` 输出只读参数。<br /><br /> 指定执行的命令提供的退出代码。 如果任务记录了任何错误，但进程的退出代码为 0（成功），则这设置为 -1。 |
| <xref:Microsoft.Build.Utilities.ToolTask.LogStandardErrorAsError%2A> | 选项 `bool` 参数。<br /><br /> 如果是 `true`，则在标准错误流上收到的所有消息都记录为错误。 |
| <xref:Microsoft.Build.Utilities.ToolTask.LogStandardErrorAsError%2A> | 可选 `bool` 参数。<br /><br /> 如果是 `true`，则在标准错误流上收到的所有消息都记录为错误。 |
| <xref:Microsoft.Build.Utilities.ToolTask.StandardErrorImportance%2A> | 可选 `String` 参数。<br /><br /> 用于从标准输出流记录文本的重要性。 |
| <xref:Microsoft.Build.Utilities.ToolTask.StandardOutputImportance%2A> | 可选 `String` 参数。<br /><br /> 用于从标准输出流记录文本的重要性。 |
| <xref:Microsoft.Build.Utilities.ToolTask.Timeout%2A> | 可选 `Int32` 参数。<br /><br /> 指定终止任务可执行文件之前的时间量（以毫秒为单位）。 默认值是 `Int.MaxValue`，指示没有超时期限。 超时以毫秒为单位。 |
| <xref:Microsoft.Build.Utilities.ToolTask.ToolExe%2A> | 可选 `string` 参数。<br /><br /> 项目可能会实现此参数以重写 ToolName。 任务可能会重写此参数以保留 ToolName。 |
| <xref:Microsoft.Build.Utilities.ToolTask.ToolPath%2A> | 可选 `string` 参数。<br /><br /> 指定任务从中加载基础可执行文件的位置。 如果未指定此参数，则任务会使用与运行 MSBuild 的框架版本对应的 SDK 安装路径。 |
| <xref:Microsoft.Build.Utilities.ToolTask.UseCommandProcessor%2A> | 可选 `bool` 参数。<br /><br /> 设置为 `true` 时，此任务会为命令行创建一个批处理文件，并使用命令处理器执行它（而不是直接执行命令）。 |
| <xref:Microsoft.Build.Utilities.ToolTask.YieldDuringToolExecution%2A> | 可选 `bool` 参数。<br /><br /> 设置为 `true` 时，此任务会在其任务执行时生成节点。 |
