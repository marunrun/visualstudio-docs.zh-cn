---
title: 性能会话概述 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools, performance session
- performance sessions
ms.assetid: 35752f95-a57a-4def-b64d-cf4899669e99
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 545a77791d7bc5318dc17d869c510fb4e8a0787f
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73189344"
---
# <a name="performance-session-overview"></a>性能会话概述
本概述说明分析的基础知识。 刚接触性能工作的开发者会了解 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具如何帮助他们快速提高工作效率以及提高其代码的性能。 在分析方面经验丰富的开发者可以获得特定分析工具功能和过程的概述。

 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具可帮助确定源代码中的性能问题并比较可能解决方案的性能。 分析工具向导和默认设置可使你立即深入了解许多性能问题。 分析工具的功能和选项可提供对探查过程的精确控制。 此控制包括精确确定代码段目标、收集数据块级别计时信息以及在数据中包含其他处理器和系统性能数据。

 以下步骤组成了使用分析工具的基本过程：

1. 通过指定收集方法和要收集的数据来配置性能会话。

2. 通过在性能会话中运行应用程序来收集分析数据。

3. 分析数据以确定性能问题。

4. 在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 集成开发环境 (IDE) 中修改代码以提高代码的应用程序性能

5. 对已更改代码收集分析数据，并比较原始数据和已更改数据的分析数据。

6. 生成记录性能提高的报告。

   若要使用分析提供的信息，应具有可用于要分析的二进制文件和 Windows 操作系统的二进制文件的符号信息。

## <a name="configure-the-performance-session"></a>配置性能会话
 若要配置分析会话，请选择要使用的分析方法和要收集的数据。 分析工具**性能向导**可以引导你完成基本配置，你可以使用性能会话属性页添加更多选项：

- 分析方法包括采样、跟踪和内存分配。

- 数据值包括时间、处理器和操作系统性能计数器以及应用程序事件（如页面错误和内核转换）。

  可以在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 项目中配置性能会话作为项目解决方案的一部分，也可以通过 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE 分析任意二进制文件。 可以在性能会话属性页中指定会话属性，也可以使用分析向导。

## <a name="collect-profiling-data"></a>收集分析数据
 从“性能资源管理器”  开始收集分析数据。 可以暂停和恢复分析以限制收集的数据量。 还可以附加到已在运行的进程。

 应用程序启动之后，“数据收集控件”  窗口会立即出现在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE 中。 从“数据收集控件”  窗口，可以通过暂停和恢复收集过程来分析应用程序的特定部分。 还可以使用“数据收集控件”  窗口将标记插入到收集的数据中。 标记是用户定义的数据点，在配置文件视图中显示，可以用于筛选分析数据。

 当目标应用程序关闭时，分析工具会生成分析数据文件 (*.vsp)，并在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE 中显示“摘要报告”视图。

## <a name="analyze-the-data-and-identify-performance-issues"></a>分析数据并确定性能问题
 结束分析运行时，数据会进行分析，摘要会显示在分析工具“性能报告”  视图窗口中。 会为目标应用程序的调用堆栈和各个函数收集分析数据。 报告视图显示应用程序的进程、线程、模块、函数和源代码行的数据范围的性能分析。 函数的分析数据值包括以下这些：

- 在函数以及函数调用的子函数中所用的总时间（非独占值）。

- 仅执行函数中的代码所用的时间（独占值）。

  通过十二个以上的不同视图可以采用最高效的方式对分析数据进行分析。 通过视图自定义可以对数据进行筛选和排序以查找可能会导致性能问题的函数。 热路径筛选可在调用树和模块视图中立即突出显示最活跃的路径。

## <a name="modify-the-application-code"></a>修改应用程序代码
 将一个或多个相关性能问题隔离出来之后，可以使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE 修改代码，然后对更改收集分析数据。

## <a name="collect-profiling-data-again-and-compare-the-data-between-the-profiling-runs"></a>再次收集分析数据并比较分析运行之间的数据
 分析工具比较报告视图显示在两个所选分析数据文件之间，模块、函数或行性能中的差异。 可以指定要比较的分析数据值，并且可以在比较视图与单个文件的视图之间进行切换。

## <a name="generate-a-report-of-the-results"></a>生成结果的报告
 可以将任何性能报告视图的行粘贴到电子邮件和电子表格中，并且可以生成包含一个或多个视图的数据的报告。

## <a name="see-also"></a>请参阅
- [概述](../profiling/overviews-performance-tools.md)
- [演练：确定性能问题](beginners-guide-to-cpu-sampling.md)