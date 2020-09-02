---
title: 内存管理时间 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.paging
helpviewer_keywords:
- Concurrency Visualizer, Paging Time
ms.assetid: 67af3509-3a7d-435d-bc37-5262448da915
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 48cbdd523f4527af84c52366a439a18330e1828c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157351"
---
# <a name="memory-management-time"></a>内存管理时间
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

时间线中的这些段与归类为内存管理的阻塞时间关联。 这意味着线程被与内存管理操作（如分页）关联的事件所阻止。 在此时间内，线程被阻止在并发可视化工具视为内存管理的 API 或内核状态下。 这些包括诸如分页和内存分配这类事件。  
  
 检查关联的调用堆栈和分析报告，以便更好地了解归类为内存管理的阻塞的基本原因。  
  
## <a name="see-also"></a>另请参阅  
 [“线程”视图](../profiling/threads-view-parallel-performance.md)
