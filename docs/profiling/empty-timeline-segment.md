---
title: 空时间线分段 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.empty
helpviewer_keywords:
- Concurrency Visualizer, empty timeline segment
ms.assetid: f37b301f-3edc-4e56-8084-feec2dc5a9b1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a96cdc7ae4edc7ea7193d5b95dfc73fa1747c1fb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62970104"
---
# <a name="empty-timeline-segment"></a>空时间线分段
在并发可视化工具中，时间线部分为空（具有白色背景）的原因取决于通道的种类。

- 对于 CPU 线程通道，这意味着在时间线的这一部分，线程不存在。 如果您需要查看线程，则可以使用缩放控件或通过水平滚动来查找其执行部分。

- 对于 I/O 通道，这意味着在该时间点未代表目标进程发生磁盘访问。

- 对于 DirectX 通道，这意味着在时间线的这一部分，未代表目标进程执行任何 GPU 工作。

- 对于标记通道，这意味着未生成任何标记。

## <a name="see-also"></a>请参阅
- [线程视图](../profiling/threads-view-parallel-performance.md)
- [缩放控件（线程视图）](../profiling/zoom-control-threads-view.md)