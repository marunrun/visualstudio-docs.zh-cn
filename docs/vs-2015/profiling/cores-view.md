---
title: “核心”视图 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.view.cores
helpviewer_keywords:
- Concurrency Visualizer, Cores View
ms.assetid: e47af672-9785-4899-bd45-4d9dda3c396f
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 869980fe7bbb773d566dffd38088b003e3a97a3d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68145637"
---
# <a name="cores-view"></a>内核视图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

内核视图显示线程执行如何映射到逻辑处理器内核。 如果要编写服务器应用程序，则此视图可以帮助您通过使用线程关联或线程池管理来优化缓存性能。 如果在使用线程关联之后实际上加剧了跨核迁移问题，则此视图还可帮助您以直观方式检查相关情况。 内核视图包括关系图和图例两个部分。  
  
 关系图在 Y 轴上显示逻辑内核，而在 X 轴上显示时间。 关系图中的每个线程都具有唯一的颜色，以便您可以跟踪它随时间跨核心移动的情况。 通过在图例区域中选择线程，您可以在此关系图中筛选它们。  
  
 图例区域中具有关系图中每种颜色的对应项。 每个项各自显示线程颜色和名称、跨核心上下文切换数、上下文切换的总数，以及跨越核心的上下文切换所占的百分比。 图例按跨核心的上下文切换数以降序排序。 它仅会列出在显示的时间范围内执行的线程。  缩放或平移后，将更新列表。  
  
## <a name="see-also"></a>另请参阅  
 [并发可视化工具](../profiling/concurrency-visualizer.md)   
 [使用率视图](../profiling/utilization-view.md)   
 [“线程”视图](../profiling/threads-view-parallel-performance.md)
