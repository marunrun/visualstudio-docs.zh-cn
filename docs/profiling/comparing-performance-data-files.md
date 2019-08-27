---
title: 比较性能数据文件 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, comparing profiling tools report files
- profiling tools reports, comparing
ms.assetid: e6fda144-f21d-4912-9d16-1b8d3555a210
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9802bc92a857192ce144432114a8add2c1becba8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62788514"
---
# <a name="compare-performance-data-files"></a>比较性能数据文件

凭借分析工具数据文件比较功能，可以选择两个报表文件（.vsp 或 .vsp 文件）并生成报告，显示从一个分析会话到另一个分析会话出现的差异、性能回归和改进。

来自 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具中的数据文件比较报告将一个分析数据文件中的分析结果与另一个数据文件中的基线分析的结果进行比较。 必须已使用同一分析方法生成了这两个数据文件。 将分析的比较报告另存为 .vsps 文件。

比较报告视图呈现已更改数据的表视图。 该表呈现增量，或基线中的更改。 增量是通过确定旧值、基线值和新分析中的结果值之间的差异来计算的。

探查器数据的比较可基于代码中的函数、应用程序中的模块、行、指令指针 (IP) 和类型。

可用于比较的分析数据包括列中显示的信息。 有关这些列名的定义，请参阅[性能报告视图](../profiling/performance-report-views.md)。

可设置阈值以降噪并筛选出未按指定量更改的行的比较表视图中的任何数据。

## <a name="in-this-section"></a>本节内容

[如何：比较性能数据文件](../profiling/how-to-compare-performance-data-files.md)