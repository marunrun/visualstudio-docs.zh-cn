---
title: 性能资源管理器 | Microsoft Docs
ms.date: 06/19/2017
ms.topic: conceptual
f1_keywords:
- vs.performance
- vs.performance.wizard.website
helpviewer_keywords:
- performance tools [Visual Studio ALM]
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 89399d49909e1c9067723e75a1adbaa123865758
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74778474"
---
# <a name="performance-explorer"></a>性能资源管理器

使用 Visual Studio 分析工具，开发人员可以衡量、评估并着力解决代码中与性能相关的问题。 这些工具已完全集成到 IDE 从而提供无缝且易于获取的用户体验。

分析应用程序非常简单。 首先创建一个新的性能会话。 在 Visual Studio Team System Development Edition 中，可以使用性能会话向导创建新的性能会话。 性能会话结束后，分析期间收集的数据将保存到 .vsp 文件中  。 可在 IDE 内部查看 .vsp 文件  。 存在几个可用的报告视图，可帮助直观显示和检测收集的数据的性能问题。

可从命令行使用分析工具。 这为用户提供了一种灵活性，即可从命令行运行这些工具或使用它们来自动执行使用脚本的任务。

有关与性能和分析相关的当前和高级主题的详细信息，可搜索 Microsoft Developer Network 查看主题和 Microsoft 博客了解相关信息。 使用关键字：企业性能工具团队。

## <a name="common-tasks"></a>常见任务

|任务|相关内容|
|----------|---------------------|
|**Windows 8 和更高版本的技术**|[Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)|
|**了解分析概念：** 了解使用分析工具收集、查看和分析代码性能的过程中将用到的概念和术语。|[概述](../profiling/overviews-performance-tools.md)|
|**投入进来然后执行此操作：** 了解使用分析工具收集、查看和分析代码性能时将用到的基本过程。 通过实际演练进行尝试。|[入门](../profiling/getting-started-with-performance-tools.md)|
|**配置分析会话：** 了解用于指定要分析的项目或二进制文件、选择分析方法、选择要收集的性能数据及设置其他分析会话选项的的高级方法。|[配置性能会话](../profiling/configuring-performance-sessions.md)|
|**控制探查器收集的数据：** 了解如何使用性能会话属性和交互式过程来启动和停止分析，以及如何将搜集的性能数据限制为所需的信息。|[控制数据收集](../profiling/controlling-data-collection.md)|
|**查找性能问题：** 了解如何查看和分析“分析工具报表”视图窗口中的收集的性能数据。|[分析性能工具数据](../profiling/analyzing-performance-tools-data.md)|
|**分析性能变化：** 了解如何比较两个探查器数据文件以分析性能变化。|[比较性能数据文件](../profiling/comparing-performance-data-files.md)|
|**保存和共享结果：** 了解如何保存分析数据以便进行存档或共享。|[保存和导出性能工具数据](../profiling/saving-and-exporting-performance-tools-data.md)|
|**自动分析：** 了解如何从命令提示符使用分析工具。|[通过命令行进行分析](../profiling/using-the-profiling-tools-from-the-command-line.md)|
|**以编程方式控制分析：** 了解如何使用托管的和本机分析工具 API 控制直接收集自源代码的数据。|[分析工具 API](../profiling/profiling-tools-apis.md)|
|**分析问题疑难解答**|[性能工具问题疑难解答](../profiling/troubleshooting-performance-tools-issues.md)|

## <a name="see-also"></a>请参阅

[首先了解分析工具](../profiling/profiling-feature-tour.md)
