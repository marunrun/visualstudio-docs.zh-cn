---
title: 抢占时间 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.preemption
helpviewer_keywords:
- Concurrency Visualizer, Preemption Time
ms.assetid: 6b78f91e-a006-440c-83fb-e7368040951d
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6fd209f65464126650106eb4509cd3de39ad8c25
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68198065"
---
# <a name="preemption-time"></a>抢占时间
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

时间线中的这些段与归类为“抢占”的阻塞时间关联。 此类别表示由于以下原因之一断开线程：  
  
- 计划程序使用更高优先级的线程将其替换。  
  
- 线程的执行量程过期，且其他线程已作好执行准备。  
  
  在此时间内，由于并发可视化工具被视为“抢占”这一内核等待原因，已阻止线程。 当线程被排出逻辑核心时，抢占段开始；当线程继续执行时，抢占段结束。  
  
  抢占段的工具提示会显示导致抢占的进程或线程的名称。 然而，这并不表示接管的进程或线程在抢占期间内会实际运行。  
  
## <a name="see-also"></a>另请参阅  
 [线程视图](../profiling/threads-view-parallel-performance.md)
