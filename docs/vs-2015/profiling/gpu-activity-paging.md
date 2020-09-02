---
title: GPU 活动(分页) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.gpuactivity
- vs.cv.threads.timeline.gpupaging
ms.assetid: 95284ac5-3492-4f7b-a79f-7d2840a07679
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5979ccf8cafedb849b7ae9f7af6b0b35096e624f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62434158"
---
# <a name="gpu-activity-paging"></a>GPU 活动(分页)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

“线程”选项卡上的“GPU 活动(分页)”段表示 GPU 处理分页请求的时间****。  段的长度代表 GPU 处理直接内存访问 (DMA) 数据包时的持续时间。 通常，分页数据包与 CPU 和 GPU 之间的内存转移有关。  
  
 当选择某个 GPU 分页段时，“当前”  选项卡上的报告将显示所处理的 DMA 数据包的相关信息。 这包括它在与 DirectX 引擎关联的硬件队列中等待的总时间、提交 DMA 数据包的进程，以及处理数据包所需的时间。  
  
## <a name="see-also"></a>另请参阅  
 [使用率视图](../profiling/utilization-view.md)
