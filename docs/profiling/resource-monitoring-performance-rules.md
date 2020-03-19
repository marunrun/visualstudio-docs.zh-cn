---
title: 资源监控性能规则 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f0f77faf-0a05-4718-a2c5-47934be40868
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 2389c23b9089ebbdd96d337a3b47d5be9d576b4b
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74778318"
---
# <a name="resource-monitoring-performance-rules"></a>资源监控性能规则
资源监控类别中的性能消息提供有关应用程序性能的其他数据。 可以使用此数据分析性能问题。 这些规则是消息性的，针对每次分析运行报告。

|||
|-|-|
|[DA0501：所分析的进程的平均 CPU 使用率。](../profiling/da0501-average-cpu-consumption-by-the-process-being-profiled.md)|此消息报告处理器忙于执行应用程序指令的时间的百分比。 报告的值是所分析的进程处于活动状态的所有测量时间间隔的平均值。|
|[DA0502：所分析的进程的 CPU 最大消耗量](../profiling/da0502-maximum-cpu-consumption-by-the-process-being-profiled.md)|此消息报告处理器忙于执行应用程序指令的时间的最大百分比。 报告的值是所分析的进程在其中处于活动状态的所有测量间隔中报告的最大值。|
|[DA0503：所分析的进程的平均工作集（以字节为单位）](../profiling/da0503-average-working-set-in-bytes-for-the-process-being-profiled.md)|此消息报告分析处于活动状态时进程使用的平均物理内存量（以字节为单位）。 此物理内存度量值称作“工作集”。|
|[DA0504：所分析的进程的最大工作集（以字节为单位）](../profiling/da0504-maximum-working-set-in-bytes-for-the-process-being-profiled.md)|此消息报告分析处于活动状态时进程使用的最大物理内存量（以字节为单位）。|
|[DA0505：为所分析进程分配的平均专用字节数](../profiling/da0505-average-private-bytes-allocated-for-the-process-being-profiled.md)|此消息报告分析处于活动状态时进程分配的平均虚拟内存量（以字节为单位）。 此虚拟内存度量值称作“专用字节”  。 专用字节表示由进程分配的虚拟内存位置，只能通过进程内部运行的线程访问此进程。|
|[DA0506：为所分析的进程分配的最大专用字节数](../profiling/da0506-maximum-private-bytes-allocated-for-the-process-being-profiled.md)|此消息报告分析处于活动状态时进程分配的最大虚拟内存量（以专用字节为单位）。|
