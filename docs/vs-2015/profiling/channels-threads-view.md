---
title: 通道（“线程”视图）| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.channelnames
helpviewer_keywords:
- Concurrency Visualizer, Channels (Threads View)
ms.assetid: 2f798c17-2363-42a4-be94-a5751d208eac
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: df93a87285bdf1172e75b63ed956c1aa978fc71e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545530"
---
# <a name="channels-threads-view"></a>通道（线程视图）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

并发可视化工具显示四类通道：线程通道、磁盘通道、标记通道和 GPU 通道。  
  
## <a name="thread-channels"></a>线程通道  
 线程通道通过颜色显示一个线程的状态。 停在通道名称处时，将显示给定线程的开始函数。 并发可视化工具可检测到多种线程。 下表列出了最常用的线程类型。  
  
|线程|描述|  
|-|-|  
|主线程|启动应用的线程。|  
|工作线程|由应用程序主线程创建的线程。|  
|CLR 工作线程|由公共语言运行时 (CLR) 创建的工作线程。|  
|调试器帮助程序|由 Visual Studio 调试器创建的工作线程。|  
|ConcRT 线程|由 Microsoft 并发运行时创建的线程。|  
|GDI 线程|由 GDIPlus 创建的线程。|  
|OLE/RPC 线程|作为 RPC 工作线程创建的线程。|  
|RPC 线程|作为 RPC 线程创建的线程。|  
|Winsock 线程|作为 Winsock 线程创建的线程。|  
|线程池|由 CLR 线程池创建的线程。|  
  
## <a name="disk-channels"></a>磁盘通道  
 磁盘通道对应于计算机中的物理驱动器。 由于系统上的每个物理驱动器均存在单独读取和编写操作通道，因此每个驱动器均有两个通道。 磁盘数量对应于内核设备名称。 只有在磁盘上有活动时才显示磁盘通道。  
  
## <a name="marker-channels"></a>标记通道  
 标记通道对应于由应用及其所使用的库生成的事件。 例如，任务并行库、并行模式库和 C++ AMP 生成显示为标记的事件。 每个标记通道关联一个线程 ID，在通道的说明旁边显示。 此 ID 用于标识生成事件的线程。 通道的说明包括生成事件的 Windows 事件跟踪 (ETW) 提供程序的名称。 如果通道显示来自[并发可视化工具 SDK](../profiling/concurrency-visualizer-sdk.md) 的事件，则还会显示该系列的名称。  
  
## <a name="gpu-channels"></a>GPU 通道  
 GPU 通道显示系统上有关 DirectX 11 活动的信息。  每个与图形卡关联的 DirectX 引擎都有一个单独的通道。  单独的段表示处理 DMA 数据包所花费的时间。  
  
## <a name="see-also"></a>另请参阅  
 [线程视图](../profiling/threads-view-parallel-performance.md)
