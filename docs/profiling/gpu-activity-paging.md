---
title: GPU 活动(分页) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.gpuactivity
- vs.cv.threads.timeline.gpupaging
ms.assetid: 95284ac5-3492-4f7b-a79f-7d2840a07679
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8bd28c7b41a01992ad52fa343b098b0a02460806
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62969610"
---
# <a name="gpu-activity-paging"></a>GPU 活动(分页)
“线程”选项卡上的“GPU 活动(分页)”段表示 GPU 处理分页请求的时间。  段的长度代表 GPU 处理直接内存访问 (DMA) 数据包时的持续时间。 通常，分页数据包与 CPU 和 GPU 之间的内存转移有关。

 当选择某个 GPU 分页段时，“当前”选项卡上的报告将显示所处理的 DMA 数据包的相关信息。 这包括它在与 DirectX 引擎关联的硬件队列中等待的总时间、提交 DMA 数据包的进程，以及处理数据包所需的时间。

## <a name="see-also"></a>请参阅
- [使用率视图](../profiling/utilization-view.md)