---
title: 演练：使用采样进行命令行分析 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, walkthroughs
- performance tools, walkthroughs
- performance tools, command-line tools
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 09272c8cf2dff02d3be024b9c3eeab8b51f56df7
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74777967"
---
# <a name="walkthrough-command-line-profiling-using-sampling"></a>演练：使用采样进行命令行分析

本演练演示如何使用命令行工具和采样功能分析应用程序以确定性能问题。

在本演练中，你将使用命令行工具逐步完成分析托管应用程序的过程，并使用采样来隔离和确定应用程序中的性能问题。

在本演练中，你将遵循以下步骤：

- 通过使用命令行工具和采样功能分析应用程序。
- 分析被采样的分析结果，以便查找并修复性能问题。

## <a name="prerequisites"></a>系统必备

- [!INCLUDE[csharp_current_short](../misc/includes/csharp_current_short_md.md)] 中级理解
- 使用命令行工具的中级理解
- [PeopleTrax 示例](performance-explorer.md)的副本
- 若要使用分析提供的信息，最好有可用的调试符号信息。

## <a name="command-line-profiling-using-the-sampling-method"></a>使用采样方法进行命令行分析

采样是一种分析方法，通过此方法可定期轮询有特定进程以确定活动函数。 生成的数据提供对进程进行采样时，函数位于调用堆栈顶部的频率计数。

> [!NOTE]
> 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。

### <a name="to-profile-the-peopletrax-application-by-using-the-sampling-method"></a>使用采样方法分析 PeopleTrax 应用程序

1. 安装 PeopleTrax 示例应用程序并生成此应用程序的发布版本。

2. 打开命令提示符窗口，然后向本地路径环境变量添加分析工具目录。

3. 将工作目录更改为包含 PeopleTrax 二进制文件的目录。

4. 键入以下命令设置相应的环境变量：

    ```cmd
    VSPerfCLREnv /sampleon
    ```

5. 通过运行 VSPerfCmd.exe 开始进行分析，此工具是控制探查器的命令行工具  。 以下命令在采样模式下启动应用程序和探查器：

    ```cmd
    VsPerfCmd /start:sample /output:PeopleTraxReport.vsp /launch:PeopleTrax.exe
    ```

     探查器进程启动，并附加到 PeopleTrax.exe 进程  。 探查器进程开始将收集的分析数据写入报表文件。

6. 单击“获取人员”  。

7. 单击“导出数据”  。

     记事本随即打开并显示其中包含从“PeopleTrax”  导出的数据的新文件。

8. 关闭记事本，然后关闭 **PeopleTrax** 应用程序。

9. 关闭探查器。 键入以下命令：

    ```cmd
    VSPerfCmd /shutdown
    ```

10. 使用以下命令重置环境变量：

    ```cmd
    VSPerfCLREnv /sampleoff
    ```

11. 分析数据存储在 .vsp 文件中。使用以下任一种方法分析结果  ：

    - 在 Visual Studio IDE 中打开 .vsp 文件  。

         — 或 —

    - 通过使用命令行工具 VSPerfReport.exe 生成逗号分隔值 (.csv) 文件   。 若要生成在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]IDE 外部使用的报表，请使用以下命令：

        ```cmd
        VSPerfReport <dir> PeopleTraxReport.vsp /output:<dir> /summary:all
        ```

## <a name="see-also"></a>请参阅

[性能会话概述](../profiling/performance-session-overview.md)
[来自命令行的配置文件](../profiling/using-the-profiling-tools-from-the-command-line.md)
[VSPerfCmd](../profiling/vsperfcmd.md)
[了解采样数据值](../profiling/understanding-sampling-data-values.md)
[性能报表视图](../profiling/performance-report-views.md)
