---
title: 如何：选择采样事件 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.property.sampling
helpviewer_keywords:
- clock cycles sample event
- sample events, choosing
- profiling tools, sample events
- page faults sample event
- system calls sample event
- performance counter sample event
- performance tools, sample events
ms.assetid: ce7cb734-80ac-4930-a4ef-e24395e1cc07
caps.latest.revision: 28
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 017414bdbf8e0e1a3a664782aab1ea44bda030c4
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432834"
---
# <a name="how-to-choose-sampling-events"></a>如何：选择采样事件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

默认情况下，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 分析工具按指定为由所分析的进程使用的处理器周期数的间隔收集性能数据。 间隔中的默认周期数为 10,000,000，这在 1 GH 计算机上大约 0.01 秒。 可以更改间隔中的周期数，也可以更改采样事件。 以下示例事件可用：  
  
- 时钟周期数 - 用于占用大量 CUP 的问题。  
  
- 页面错误 - 用于内存相关问题。  
  
- 系统调用数 - 用于 I/O 相关问题。  
  
- 性能计数器 - 用于低级别性能问题的 CPU 计数器。  
  
> [!IMPORTANT]
> 如果正在使用采样方法收集 .NET 内存数据（分配和/或对象生存期），将忽略所有用户指定的采样事件，且相应的内存分配和/或垃圾回收事件将用于收集数据。  
  
### <a name="to-select-a-sample-event"></a>选择样本事件  
  
1. 在“性能资源管理器” 中，右键单击性能会话，然后单击“属性” 。  
  
2. 在“属性页”中，单击“采样”属性。  
  
3. 从“示例事件”下拉列表中，选择要用于分析应用程序的示例事件。  
  
    > [!NOTE]
    > 仅当从“示例事件”下拉列表中选择“性能计数器”时，“可用的性能计数器”才会启用。  
  
4. 如果选择“性能计数器”，请从“可用的性能计数器”树视图控件中选择特定的 CPU 计数器。  
  
    - “可移植事件”节点中的计数器适用于所有类型的处理器。  
  
    - “平台事件”节点中的计数器特定于当前的计算机上的处理器，并且可能不适用于其他类型的处理器。  
  
5. 选择示例事件时，“采样间隔”文本框中将显示默认的采样间隔值。 如有必要，可在文本框中输入想要的值。  
  
## <a name="see-also"></a>请参阅  
 [配置性能会话](../profiling/configuring-performance-sessions.md)   
 [如何：选择收集方法](../profiling/how-to-choose-collection-methods.md)   
 [CPU 和 Windows 计数器](../profiling/cpu-and-windows-counters.md)   
 [了解采样数据值](../profiling/understanding-sampling-data-values.md)   
 [从命令行分析](../profiling/using-the-profiling-tools-from-the-command-line.md)
