---
title: 如何：比较性能数据文件 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vsperf.choosediffbinaries
helpviewer_keywords:
- profiling tools, how to compare profiler result files
- profiler result files, how to compare
ms.assetid: 1905b45d-c6b3-43c8-87b1-1aee734f37f9
caps.latest.revision: 25
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 185494623e019ef666374bd46e52bca0d58738f4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68185939"
---
# <a name="how-to-compare-performance-data-files"></a>如何：比较性能数据文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以创建比较（“差异”）报表或视图来比较两个不同的探查器数据文件（.vsp 或 .vsps）的结果。 比较显示从一个分析会话到另一个分析会话所发生的差异、性能回归和改进。  
  
 “差异”报表呈现数据的表视图。 该表呈现增量，或基线中的更改。 这是通过确定新分析中的旧值、基线值和结果值之间的差异来计算的。  
  
 探查器数据的比较可基于代码中的函数、应用程序中的模块、行、指令指针 (IP) 和类型。  
  
 可设置阈值以降噪并筛选出未按指定量更改的行的表视图中的任何数据。  
  
### <a name="to-create-comparison-file-view-for-a-project-in-performance-explorer"></a>在“性能资源管理器”中为项目创建比较文件视图  
  
1. 在 **性能资源管理器**中的 " **报表**" 下，选择要用作比较基线值的 .vsp 或 .vsps 报表文件。  
  
2. 选择要比较的 .vsp 或 .vsps 报表文件。  
  
3. 右键单击其中一个所选文件，然后单击“比较报告”。  
  
### <a name="to-compare-values"></a>比较值  
  
1. 在“报表视图”窗口中选择“比较报告”。  
  
2. 在“表”下拉列表中，选择要比较的函数或模块。  
  
3. 在“列”下拉列表中，选择要比较的值。  
  
4. （可选）键入“阈值”的值。  
  
5. 单击“应用”。  
  
### <a name="to-compare-report-files"></a>比较报表文件  
  
1. 在“分析”菜单上，选择“比较性能报告”。  
  
2. 在 " **选择要比较的分析文件** " 窗口中，浏览并选择 **基准文件** 分析文件 ( .vsp 或 .Vsps) 以及 **比较文件** ( .vsp 或 .vsps) 。  
  
3. 单击 **“确定”** 。
