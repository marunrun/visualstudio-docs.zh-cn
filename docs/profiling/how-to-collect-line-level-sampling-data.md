---
title: 如何：收集行级采样数据 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- performance tools, line-level sampling
ms.assetid: 44803aad-dd39-4c2e-9209-d35185d44983
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: f64040c9180a152650de16b23276ab0e65cc9ead
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74776353"
---
# <a name="how-to-collect-line-level-sampling-data"></a>如何：收集行级采样数据
行级采样是探查器确定占用大量处理器时间的函数在代码中的位置，如具有高独占样本的函数，处理器需要耗费大量时间。

## <a name="overview"></a>概述
 对于行级采样，探查器可按设定间隔引导程序调用堆栈，并聚合这些结果。 这些结果显示在获取样本时处理器正在执行的指令。 然后会对关于独占样本的已收集数据进行分析以确定代码行和指令指针 (IP)。

 行级采样适用于托管代码和本机代码。 显示此数据的性能报告包括“行”视图和“模块”视图。

 字符开始/结束信息不适用于本机代码。 对于多行语句，行开始信息不适用于本机代码；仅行结束信息适用。

### <a name="available-data"></a>可用数据
 可用的行级采样数据包括以下信息：

- 函数名称。

- 函数地址。

- 行开始 – 被采样代码的行号。

- 行结束 – 结束源行号。 除单个程序语句跨多个源代码行的情况外，这通常与“行开始”数据相同。

- 字符开始 – 聚合样本的开始列。 除单个程序语句跨多个源代码行的情况外，这通常为 0。

- 字符结尾 – 聚合样本的结束列。

- IP - 获取聚合样本的地址（仅限 IP 视图）。

  在“模块”  视图中，如果函数具有行级统计信息，这些统计信息将嵌套在每个函数下。 此外，还将显示嵌套在每行下的 IP 级统计信息。

### <a name="turn-off-line-level-sampling-for-managed-code"></a>关闭托管代码的行级采样
 默认情况下，行级采样处于开启状态。 可以使用以下任一命令来关闭托管代码的行级数据收集：

- 分析前，键入 **VSPerfCLREnv /samplelineoff**。 这会影响应用程序和服务。

     — 或 —

- 启动应用程序时，键入 **VSPerfCmd /lineoff \<其他参数>** 。

## <a name="see-also"></a>另请参阅
- [配置性能会话](../profiling/configuring-performance-sessions.md)
- [分析性能工具数据](../profiling/analyzing-performance-tools-data.md)
