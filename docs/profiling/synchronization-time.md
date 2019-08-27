---
title: 同步时间 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.synchronization
helpviewer_keywords:
- Concurrency Visualizer, Synchronization Time
ms.assetid: affa04cc-8bba-4848-9301-b19846d3c2cb
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ae73f7b9a9838a006dce47bf44b0ed46aa0b84fa
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62965305"
---
# <a name="synchronization-time"></a>同步时间
时间线中的这些段与归类为同步的阻止时间关联。 当线程被标记为在同步中阻止时，表示出现了下列情况之一：

- 执行该线程可能会导致调用已知线程同步 API（如 `EnterCriticalSection()` 或 `WaitForSingleObject()`）。

- API 匹配算法无法做到非常全面，因此一些可映射到其他类别的 API 也可能显示为同步，这是因为调用堆栈中的帧会最终到达映射到此类别的基础内核阻止基元。

  若要了解线程阻止事件的基本原因，可仔细检查阻止调用堆栈和分析报告。

## <a name="see-also"></a>请参阅
- [“线程”视图](../profiling/threads-view-parallel-performance.md)