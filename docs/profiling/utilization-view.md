---
title: 使用率视图 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.cpuutilization
helpviewer_keywords:
- Concurrency Visualizer, CPU Utilization View
ms.assetid: b4f7ceab-3653-4069-bb74-c309aec62866
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 926c67261f91aa8787d9be4a33dadbd3a890c568
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62823514"
---
# <a name="utilization-view"></a>“使用率”视图
“使用率”视图显示有关当前进程所使用的 CPU、GPU 和其他系统资源的信息（选择“分析” > “并发可视化工具”来启动并发可视化工具）。 它显示随着时间的推移，在系统上运行的分析的进程、空闲进程、系统进程和其他进程的平均核心使用率。 它不显示在某个给定时间哪个特定内核处于活动状态。 例如，如果两个内核在某一给定时间段内均以 50% 的使用率运行，则此视图将显示使用一个逻辑内核。 通过将分析时间分成较短的时间段生成此视图。 对于每个时间段，此图绘制出该间隔期间内在逻辑核心上执行的进程线程的平均数量。

 ![CPU 使用率视图](../profiling/media/vsts_ppacpuutil.png "VSTS_PPAcpuUtil")

 此图显示目标进程、空闲进程和系统进程所使用的时间（在 x 轴上）和平均的逻辑核心数量。 （空闲进程显示空闲内核。 系统进程是 Windows 中可代表其他进程执行工作的进程。）在系统上运行的剩余进程组成了所有剩余核心的使用率。

 逻辑核心数显示在 Y 轴上。 Windows 将硬件中的多线程并行处理支持视为逻辑核心（例如，超线程）。 因此，具有 4 核处理器且每核心支持两个硬件线程的系统显示为 8 逻辑核心的系统。 这同样也适用于“核心”视图。 有关详细信息，请参阅[“核心”视图](../profiling/cores-view.md)。

 GPU 活动关系图显示随着时间的推移，使用中的 DirectX 引擎数。  如果引擎正在处理 DMA 数据包，它则正在使用中。  该关系图不会显示特定的 DirectX 引擎（例如，3D 引擎、视频引擎等）。

## <a name="purpose"></a>目标
 我们建议在使用并发可视化工具时，将使用率视图作为性能调查的起点。 因为它概述了随着时间的推移，应用中的并发程，因此，可使用它快速识别需要进行性能调整或并行化的区域。

 如果对性能调整感兴趣，则可尝试识别不满足你期望的行为。 还可查找逻辑 CPU 核心使用率低的区域及原因。 此外，也可以查找 CPU 和 GPU 之间的使用模式。

 如果对并行化应用感兴趣，则可能会查找执行所占用大量 CPU 的区域或未使用 CPU 的区域。

 占用大量 CPU 的领域为绿色。 如果应用为串行，该图表则显示正在使用中的一个核心。

 未使用 CPU 的区域为灰色。 这些可能表示应用处于空闲状态或执行阻塞 I/O 的点，后者通过与其他占用大量 CPU 的工作重叠以提供进行并行的机会。

 找到感兴趣的行为后，可以通过选中该行为在该区域上进行放大。 缩放后，可以切换到“线程”视图或“核心”视图以了解更详细的分析。

 如果是通过 C++ AMP 或 DirectX 使用 GPU，则可能会对识别使用中的 GPU 引擎数或 GPU 在其中意外处于空闲状态的区域感兴趣。

## <a name="zoom"></a>缩放
 若要在 CPU 使用率关系图或 GPU 活动关系图上放大，请选择某个节，或使用关系图顶部的缩放滑块工具。 当切换到其他视图时，缩放设置仍然存在。 若要再次缩小，请使用缩放滑块工具。 还可以使用 Ctrl+滚动条进行缩放。

## <a name="see-also"></a>请参阅
- [并发可视化工具](../profiling/concurrency-visualizer.md)
- [“核心”视图](../profiling/cores-view.md)