---
title: 从命令行创建探查器报告 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: c886f8af-2014-4fec-9b24-d98b68ecafb7
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 489ebd4e5aff3ef9b93ef0d8fe18f9ae8cc85011
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62537197"
---
# <a name="creating-profiler-reports-from-the-command-line"></a>从命令行创建探查器报告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 VSPerfReport 命令行工具可从分析数据 (.vsp) 文件创建 .xml 或逗号分隔值 (.csv) 报告。 VSPerfReport 报告类型非常类似基于表的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 界面视图。 可以筛选报告，使之仅显示您的代码以及分析数据文件中的一段。 有关详细信息，请参阅 [VSPerfReport](../profiling/vsperfreport.md)。  
  
 通过在 .vsp 文件中嵌入符号和创建较小且打开速度较快的预分析报告 (.vsps) 文件，还可以使共享分析数据文件变得更加容易。  
  
## <a name="common-tasks"></a>常规任务  
  
|任务|相关内容|  
|----------|---------------------|  
|创建基本报告。 创建全部或部分 VSPerfReport 报告类型。|-   [创建基本报告](../profiling/creating-basic-profiling-reports-from-the-command-line.md)|  
|比较两个分析数据文件。 创建“diff”报告，用于比较两个分析数据文件中的性能数据。|-   [如何：通过命令提示符创建探查器比较报告](../profiling/how-to-create-a-profiler-comparison-report-from-a-command-prompt.md)|  
|查看调用跟踪和 Windows 事件跟踪 (ETW) 数据。 创建调用跟踪报告，报告将列出应用程序函数每个入口点和出口点的计时信息，以及该函数对其他函数的每次调用的计时信息。 或者，创建在分析运行期间收集的所有 ETW 事件的详细列表。|-   [如何：创建调用跟踪报告](../profiling/how-to-create-a-profiling-tools-call-trace-report.md)|  
|筛选报告。 限制报告，使其仅显示代码中的函数，或仅显示分析数据文件中的特定时间。|-   [如何：通过命令行筛选报告](../profiling/how-to-filter-reports-from-the-command-line.md)|  
|创建可移植分析数据文件。 若要更轻松地共享分析数据，可以将分析运行的符号嵌入到 .vsp 文件中。 还可以创建经过预先分析的分析数据 (.vsps) 文件，此文件较小，打开速度较快。|-   [创建可移植分析数据文件](../profiling/creating-portable-profiling-data-files-from-the-command-line.md)|
