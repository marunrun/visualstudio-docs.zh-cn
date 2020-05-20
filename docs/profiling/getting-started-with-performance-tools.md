---
title: 性能工具入门 | Microsoft Docs
ms.date: 11/04/2018
ms.topic: conceptual
helpviewer_keywords:
- getting started, performance
- getting started, profiling tools
ms.assetid: 02085214-a8e4-40fd-9b26-32391a7a7082
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: faba7a6d2e698e919c0f0adca6fa574838b8b3c4
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74779202"
---
# <a name="getting-started-with-performance-tools"></a>性能工具入门

Visual Studio 提供了几种收集、查看和分析代码性能数据的方法。 在许多情况下，开始使用性能工具的最佳方式是使用“性能向导”的默认设置  。 该向导收集可指出代码中性能问题的应用统计信息。

- 通知常见编码问题的性能警告显示在 Visual Studio 的“错误列表”窗口中  。 可以从警告导航到源代码和详细的帮助主题，可借助这些主题编写更高效的代码。

- 性能报告提供有关应用程序结构、源代码行和进程的不同级别的视图。 性能报告显示应用执行数据，范围从特定函数的调用和被调用函数到整个应用的调用树。

若要快速分析项目、应用或 ASP.NET 网站，请选择“调试” > “性能探查器”，然后选择“性能向导”。 有关详细说明，请参阅[性能分析初学者指南](../profiling/beginners-guide-to-cpu-sampling.md)和[如何：收集网站的性能数据](../profiling/how-to-collect-performance-data-for-a-web-site.md)。

若要手动指定和配置性能分析会话，请选择“调试” > “探查器” > “性能资源管理器”。 使用“性能资源管理器”中的“目标”文件夹和“属性”页面来配置会话。 有关说明，请参阅[如何：手动创建性能会话](../profiling/how-to-manually-create-performance-sessions.md)。

**另请参阅：**

- [性能工具概述](../profiling/overviews-performance-tools.md)
- [分析性能工具数据](../profiling/analyzing-performance-tools-data.md)
- [使用性能规则对数据进行分析](../profiling/using-performance-rules-to-analyze-data.md)
- [配置性能会话](../profiling/configuring-performance-sessions.md)
