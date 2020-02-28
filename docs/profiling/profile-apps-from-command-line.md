---
title: 从命令行测量性能
description: 从命令行测量应用程序中的 CPU 性能和托管内存使用情况。
ms.custom: ''
ms.date: 02/21/2020
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools, command-line
- Diagnostics Tools, command-line
- CPU Usage, command-line
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: c109e2ae1db28f8e08ed7c34a7ee0871a6efe670
ms.sourcegitcommit: bf2e9d4ff38bf5b62b8af3da1e6a183beb899809
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2020
ms.locfileid: "77558122"
---
# <a name="measure-application-performance-from-the-command-line"></a>从命令行测量应用程序性能

可以使用命令行工具收集有关应用程序的性能信息。

在本文所述的示例中，收集 Microsoft Notepad 的性能信息，但可以使用相同的方法来分析任何进程。

## <a name="prerequisites"></a>先决条件

* Visual Studio 2019 预览版 3 或更高版本

* 熟悉命令行工具

## <a name="collect-performance-data"></a>收集性能数据

使用 Visual Studio 诊断 CLI 工具进行性能分析的工作原理是将性能分析工具与其中某个收集器代理一起附加到进程。 附加性能分析工具时，将开始诊断捕获并存储分析数据的会话，直到该工具停止，此时数据将导出到 .diagsession 文件中。 然后，可以在 Visual Studio 中打开此文件以分析结果。

1. 启动 Notepad，并打开任务管理器来获取其进程 ID (PID)。 在任务管理器中，找到“详细信息”选项卡中的 PID。

1. 打开命令提示符，切换到包含集合代理可执行文件的目录（通常在此处）。

   ```<Visual Studio installation folder>\2019\Preview\Team Tools\DiagnosticsHub\Collector\```

1. 通过键入以下命令，启动 VSDiagnostics.exe。

   ```cmd
   VSDiagnostics.exe start <id> /attach:<pid> /loadConfig:<configFile>
   ```

   必须包含的参数是：

   * \<id> 标识集合会话。 ID 必须为介于 1 - 255 之间的数字。
   * \<pid>，要分析的进程的 PID 在本例中是在步骤 1 中找到的 PID
   * \<configFile>，要启动的集合代理的配置文件。 有关详细信息，请参阅[代理的配置文件](#config_file)。

1. 重设 Notepad 大小，或在其中键入内容，以确保收集一些有趣的分析信息。

1. 通过键入以下命令，停止收集会话并将输出发送到文件。

   ```cmd
   VSDiagnostics.exe stop <id> /output:<path to file>
   ```

1. 转到上一个命令的文件输出，并在 Visual Studio 中打开它以检查收集的信息。

## <a name="config_file"></a> 代理配置文件

集合代理是可互换的组件，可根据要测量的内容收集不同类型的数据。

为方便起见，可以将该信息存储在代理配置文件中。 配置文件是至少包含 .dll 的名称及其 COM CLSID 的 .json 文件。 以下是可以在以下文件夹中找到的示例配置文件：

```<Visual Studio installation folder>\2019\Preview\Team Tools\DiagnosticsHub\Collector\AgentConfigs\```

* CpuUsage 配置（基本/高/低），对应于为 [CPU 使用率](../profiling/cpu-usage.md)分析工具收集的数据。
* DotNetObjectAlloc 配置（基本/低），对应于为 [.NET 对象分配工具](../profiling/dotnet-alloc-tool.md)收集的数据。

基本/低/高配置是指采样率。 例如，低为 100 样本/秒，高为 4000 样本/秒。

为了 VSDiagnostics.exe 工具用于集合代理，它需要用于适当代理的 DLL 和 COM CLSID，并且代理也可能具有其他配置选项。 如果使用不带配置文件的代理，请使用以下命令中的格式。

```cmd
VSDiagnostics.exe start <id> /attach:<pid> /loadAgent:<agentCLSID>;<agentName>[;<config>]
```

## <a name="permissions"></a>权限

要分析需要提升权限的应用程序，必须从提升的命令提示符执行操作。
