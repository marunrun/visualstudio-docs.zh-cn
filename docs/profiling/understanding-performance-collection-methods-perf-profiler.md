---
title: 了解性能收集方法 | Microsoft Docs
ms.date: 4/30/2020
ms.topic: conceptual
f1_keywords: ''
helpviewer_keywords:
- Performance Profiler, profiling methods
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: '>= vs-2017'
ms.workload:
- multiple
ms.openlocfilehash: 03a49763a682f6b98b02fe40ba957efa8f5483c8
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290806"
---
# <a name="understand-performance-collection-methods"></a>了解性能收集方法

本文档概述了 Visual Studio 性能探查器中的工具所利用的数据收集方法。 

## <a name="sampling"></a>采样

采样分析方法收集有关应用程序在分析运行过程中执行的工作的统计数据。 数据收集的完成方法是：按固定间隔或采样频率（例如每毫秒）收集有关应用程序的信息，然后分析这些数据来创建在应用程序中时间花费情况的模型。 采样方法是轻量级的，对要分析的应用程序的执行几乎没有什么影响。 性能探查器中利用采样方法的工具包括 [CPU 使用率](../profiling/cpu-usage.md)工具。

## <a name="instrumentation"></a>检测

检测分析收集有关应用程序在分析运行过程中执行的工作的详细信息。 数据收集是通过工具来完成的，这些工具将代码注入到可捕获计时信息的二进制文件中，或通过使用回叫挂钩在应用程序运行期间收集和发出精确计时和调用计数信息。 与基于采样的方法相比，检测方法的开销较大。 性能探查器中使用检测的工具包括 [.NET 对象分配](../profiling/dotnet-alloc-tool.md)工具。