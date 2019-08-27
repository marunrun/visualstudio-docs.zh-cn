---
title: 如何：收集 CPU 计数器数据 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.property.cpucounters
helpviewer_keywords:
- profiling tools, using portable CPU counters
- performance tools, portable CPU counters
ms.assetid: 102fb6ca-5fbf-4b05-925f-56912ce3f44b
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 76dac6e20cc85eeb5784b0b6e29ee8d1b23fbd92
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432800"
---
# <a name="how-to-collect-cpu-counter-data"></a>如何：收集 CPU 计数器数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

CPU 事件计数器用于收集特定于硬件的性能数据。 本主题演示如何在使用检测分析方法时收集事件计数器数据。  
  
 **要求**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
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
  
### <a name="to-collect-cpu-performance-counter-data-when-you-profile-by-instrumentation"></a>通过检测进行分析时收集 CPU 性能计数器数据  
  
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
