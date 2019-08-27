---
title: GPU 活动(此进程) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.gpuexecution
- vs.cv.threads.timeline.gpuactivity
ms.assetid: 0956edbf-9bcd-4afe-9287-fda628648ca0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 68e85fc44977a3d9756965de12e25d13d62dbb89
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62969533"
---
# <a name="gpu-activity-this-process"></a>GPU 活动(此进程)
在并发可视化工具中，“线程”视图中的“GPU 活动(此进程)”段表示 GPU 代表当前进程处理请求的时间。 这些请求以直接内存访问 (DMA) 数据包的形式发送到 GPU。 段的长度代表 GPU 代表当前进程处理 DMA 数据包的时间。

 当选择 GPU 活动段时，“当前”选项卡上的报告将显示所处理的 DMA 数据包的相关信息。 此信息包括数据包在与 DirectX 引擎关联的硬件队列中等待的总时间、提交数据包的进程，以及处理数据包所需的时间。 当前进程外的某个进程可能以物理方式将 DMA 数据包提交给了 GPU。 当另一个进程代表当前进程将工作提交给 GPU 时，并发可视化工具可以检测出来。