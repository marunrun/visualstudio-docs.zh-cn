---
title: “核心”视图图例 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.cores.legend
helpviewer_keywords:
- Concurrency Visualizer, Cores View Legend
ms.assetid: e160384c-fcfe-49b3-86b7-229adb736c51
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 05f768f6ff928ab00ebbd503c1ae9826dab8cd38
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68161305"
---
# <a name="cores-view-legend"></a>内核视图图例
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

“核心”视图图例按颜色和名称标识每个线程。 它包括一些列，分别显示跨核心上下文切换数、上下文切换总数以及跨越核心的上下文切换所占的百分比。 图例中的行按跨核心上下文切换数以降序排序。  
  
 可以选择图例中的行，以便筛选时间线中显示的线程。 时间线中仅显示选定的线程。 如果未选择任何行，则时间线中将显示所有行。  
  
 与留在同一逻辑核心上的切换相比，跨核心上下文切换要花费更多的开销和性能。 在上下文切换过程中，将保存并恢复处理器寄存器，执行操作系统内核代码，重新加载转换旁视缓冲项，并刷新处理器管道。 因为缓存数据对其他核心上的此线程无效，所以跨核心上下文切换可能比其他上下文切换的开销更大。 相比之下，如果某个线程上下文切换到之前运行过该线程的核心上，则有用的数据可能仍在缓存中。 当跨核心上下文切换因试图管理线程关联而有所增加且性能出现下降时，请考虑是否要解决这一问题。 首先消除线程关联，然后观察由此导致的跨核心行为。  
  
 下表描述了图例元素。  
  
|元素|定义|  
|-------------|----------------|  
|线程名|显示上一个内核时间线中线程的颜色，以及该线程的名称。|  
|跨核心上下文切换|也从一个逻辑内核切换到另一个逻辑内核的线程的上下文切换数。 不区分从一个处理器芯片跨到另一个芯片的跨核心上下文切换，以及留在同一芯片上的跨核心上下文切换。|  
|上下文切换总数|采样期间给定线程的上下文切换总数。 每次线程更改上下文（例如从执行到同步）时，将进行一次上下文切换计数。|  
|跨越核心的上下文切换所占的百分比|通过跨核心上下文切换数除以上下文切换总数计算出的百分比。 此百分比越高，此特定线程的性能上的跨核心上下文切换的开销的整体效果越大。|  
  
## <a name="see-also"></a>另请参阅  
 [内核视图](../profiling/cores-view.md)
