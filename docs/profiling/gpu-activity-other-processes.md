---
title: GPU 活动(其他进程) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.gpuother
- vs.cv.threads.timeline.gpuactivity
ms.assetid: 8a68df65-eb63-452f-9285-fb4ffc92f2b2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9a502590c20fce1455d9259ae681178d9cd48e33
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62969497"
---
# <a name="gpu-activity-other-processes"></a>GPU 活动(其他进程)
并发可视化工具的“线程”视图中的“GPU 活动(其他进程)”  段表示 GPU 代表系统上的其他进程处理请求的时间。 这些请求以直接内存访问 (DMA) 数据包的形式发送到 GPU。  段的长度代表 GPU 处理数据包的持续时间。

 当选择此类型段时，“当前”  选项卡上的报告将显示所处理的数据包的相关信息。  此信息包括数据包在与 DirectX 引擎关联的硬件队列中等待的总时间、提交数据包的进程，以及处理数据包所需的时间。