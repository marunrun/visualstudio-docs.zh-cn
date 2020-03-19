---
title: “当前”选项卡 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.reportnav.current
helpviewer_keywords:
- Concurrency Visualizer, Callstack at Selection Point
ms.assetid: 2c7b1ae5-3756-4795-bc59-f6bb113f2ba5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f48ba44d41286f1cf5eda6ececb68d21d39abd14
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62552783"
---
# <a name="current-tab"></a>“当前”选项卡
如果选择一个 CPU 线程段，则通过单击“当前”  选项卡，可以查看时间线中最接近当前选择点的调用堆栈（如果有）。  在这种情况下，选择点由时间线上方的黑色箭头或插入符号来表示。 选择阻塞段时，将不显示插入符号，因为没有任何执行操作。 但是，仍会突出显示该段，并显示调用堆栈。

 “当前”  选项卡还显示有关 DirectX 活动段、标记和 I/O 访问的信息。  对于 DirectX 活动段，将会显示有关硬件队列如何处理 DMA 数据包的信息。  对于标记，将会显示有关说明和标记类型的信息。  对于 I/O 访问，将会显示有关文件和读取或写入字节数的信息。

## <a name="see-also"></a>另请参阅
- [“线程”视图](../profiling/threads-view-parallel-performance.md)