---
title: ToolTaskExtension 基类 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: 258ae433-f68a-49f1-b276-da20e3472e68
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 947a1df101a169b7bdad4efda74cab1ae042964a
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594963"
---
# <a name="tooltaskextension-base-class"></a>ToolTaskExtension 基类
很多任务继承自 <xref:Microsoft.Build.Tasks.ToolTaskExtension> 类，该类继承自 <xref:Microsoft.Build.Utilities.ToolTask> 类，后者本身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 此继承链向从它们派生的任务添加了几个参数。 本文档中列出了这些参数。

## <a name="parameters"></a>参数
 下表介绍基类的参数。

| 参数 | 描述 |
| - | - |
| <xref:Microsoft.Build.Utilities.Task.BuildEngine%2A> | 可选 <xref:Microsoft.Build.Framework.IBuildEngine> 参数。<br /><br /> 指定可供任务使用的生成引擎接口。 生成引擎会自动设置此参数，以允许任务回调到其中。 |
| <xref:Microsoft.Build.Utilities.Task.BuildEngine2%2A> | 可选 <xref:Microsoft.Build.Framework.IBuildEngine2> 参数。<br /><br /> 指定可供任务使用的生成引擎接口。 生成引擎会自动设置此参数，以允许任务回调到其中。<br /><br /> 这是一个便捷属性，使从此类继承的任务作者不必将值从 `IBuildEngine` 强制转换为 `IBuildEngine2`。 |
| <xref:Microsoft.Build.Utilities.Task.BuildEngine3%2A> | 可选 <xref:Microsoft.Build.Framework.IBuildEngine3> 参数。<br /><br /> 指定主机使用的生成引擎接口。 |
| <xref:Microsoft.Build.Utilities.ToolTask.EchoOff%2A> | 可选 `bool` 参数。<br /><br /> 设置为 `true` 时，此任务会将 /Q  传递到 cmd.exe  命令行，以便命令行不会复制到 stdout。 |
| <xref:Microsoft.Build.Utilities.ToolTask.EnvironmentVariables%2A> | 可选的 `String` 数组参数。<br /><br /> 环境变量对的数组（使用等号分隔）。 这些变量会传递到生成的可执行文件以及（有选择地重写）常规环境块。 |
| <xref:Microsoft.Build.Utilities.ToolTask.ExitCode%2A> | 可选 `Int32` 输出只读参数。<br /><br /> 指定执行的命令提供的退出代码。 如果任务记录了任何错误，但进程的退出代码为 0（成功），则这设置为 -1。 |
| <xref:Microsoft.Build.Utilities.Task.HostObject%2A> | 可选 <xref:Microsoft.Build.Framework.ITaskHost> 参数。<br /><br /> 指定主机对象实例（可以为 null）。 如果主机 IDE 具有与此特定任务关联的主机对象，则生成引擎会设置此属性。 |
| <xref:Microsoft.Build.Tasks.ToolTaskExtension.Log%2A> | 可选 <xref:Microsoft.Build.Utilities.TaskLoggingHelper> 只读参数。<br /><br /> 获取包含任务日志记录方法的 <xref:Microsoft.Build.Tasks.TaskLoggingHelperExtension> 类的实例。 |
| <xref:Microsoft.Build.Utilities.ToolTask.LogStandardErrorAsError%2A> | 选项 `bool` 参数。<br /><br /> 如果是 `true`，则在标准错误流上收到的所有消息都记录为错误。 |
| <xref:Microsoft.Build.Utilities.ToolTask.StandardErrorImportance%2A> | 可选 `String` 参数。<br /><br /> 用于从标准输出流记录文本的重要性。 |
| <xref:Microsoft.Build.Utilities.ToolTask.StandardOutputImportance%2A> | 可选 `String` 参数。<br /><br /> 用于从标准输出流记录文本的重要性。 |
| <xref:Microsoft.Build.Utilities.ToolTask.Timeout%2A> | 虚拟可选 `Int32` 参数。<br /><br /> 指定终止任务可执行文件之前的时间量（以毫秒为单位）。 默认值是 `Int.MaxValue`，指示没有超时期限。 超时以毫秒为单位。 |
| <xref:Microsoft.Build.Utilities.ToolTask.ToolExe%2A> | 虚拟可选 `string` 参数。<br /><br /> 项目可能会实现此参数以重写 ToolName。 任务可能会重写此参数以保留 ToolName。 |
| <xref:Microsoft.Build.Utilities.ToolTask.ToolPath%2A> | 可选 `string` 参数。<br /><br /> 指定任务从中加载基础可执行文件的位置。 如果未指定此参数，则任务会使用与运行 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 的框架版本对应的 SDK 安装路径。 |
| <xref:Microsoft.Build.Utilities.ToolTask.UseCommandProcessor%2A> | 可选 `bool` 参数。<br /><br /> 设置为 `true` 时，此任务会为命令行创建一个批处理文件，并使用命令处理器执行它（而不是直接执行命令）。 |
| <xref:Microsoft.Build.Utilities.ToolTask.YieldDuringToolExecution%2A> | 可选 `bool` 参数。<br /><br /> 设置为 `true` 时，此任务会在其任务执行时生成节点。 |

## <a name="see-also"></a>请参阅
- [任务参考](../msbuild/msbuild-task-reference.md)
- [任务](../msbuild/msbuild-tasks.md)
