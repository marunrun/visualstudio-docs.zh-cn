---
title: 如何：收集 CPU 计数器数据 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.property.cpucounters
helpviewer_keywords:
- profiling tools, using portable CPU counters
- performance tools, portable CPU counters
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c607263c6b6f6472258aaeab1c3187efaf30a120
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62973976"
---
# <a name="how-to-collect-cpu-counter-data"></a>如何：收集 CPU 计数器数据

CPU 事件计数器用于收集特定于硬件的性能数据。 本文演示如何在使用检测分析方法时收集事件计数器数据。

将发生两种类型的 CPU 计数器事件：

- 可移植事件 – 不考虑特定的 CPU，可收集的 CPU 事件。

- 平台事件 - 耦合到特定 CPU 的 CPU 事件。

  可移植事件包括常规事件，如已撤回指令和非终止的周期、CPU 缓冲区事件、分支的事件和 L2 缓存事件。 可用的平台事件计数器由处理器制造商确定。

  可在可移植计数器和平台计数器之间共享事件的类别。 例如，以下类别的数据经常适用于这两种类型：

- 内存事件。

- 前端事件。

- 分支事件。

  可以在探查器中通过两种方式收集性能计数器数据：

- 通过检测进行分析时，从一个或多个计数器中收集数据。

- 通过采样进行分析时，指定一个计数器事件作为采样间隔。 有关详细信息，请参阅[如何：选择采样事件](../profiling/how-to-choose-sampling-events.md)。

## <a name="to-collect-cpu-performance-counter-data-when-you-profile-by-instrumentation"></a>通过检测进行分析时收集 CPU 性能计数器数据

1. 在性能会话“属性页”上，单击“CPU 计数器”。

2. 选择“收集 CPU 计数器”复选框。

3. 展开“可用的性能计数器”树，然后查找想要收集的采样事件。

4. 对于想要收集的每个事件，选择该事件，然后单击右箭头以将事件添加到“所选计数器”列表。

    > [!NOTE]
    > 仅在选择“收集 CPU 计数器”复选框时，“可用的性能计数器”才会启用。

## <a name="see-also"></a>请参阅

[配置性能会话](../profiling/configuring-performance-sessions.md)
[性能会话属性](../profiling/performance-session-properties.md)
[CPU 和 Windows 计数器](../profiling/cpu-and-windows-counters.md)
[如何：选择采样事件](../profiling/how-to-choose-sampling-events.md)