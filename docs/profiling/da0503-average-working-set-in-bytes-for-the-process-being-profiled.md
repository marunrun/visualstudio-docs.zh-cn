---
title: DA0503：所分析的进程的平均工作集（字节）| Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.503
- vs.performance.DA0503
- vs.performance.rules.DA0503
ms.assetid: 9047a494-eaaf-4679-b422-c64e8bde77a4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4f2f349c4ca2172ac2be6c22f3fe999ca0a3cff0
ms.sourcegitcommit: 257fc60eb01fefafa9185fca28727ded81b8bca9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72910209"
---
# <a name="da0503-average-working-set-in-bytes-for-the-process-being-profiled"></a>DA0503：所分析进程的平均工作集（字节）

|||
|-|-|
|规则 ID|DA0503|
|类别|资源监控|
|分析方法|全部|
|消息|收集此信息仅用于参考。 进程工作集计数器测量由正在分析的进程使用的物理内存的使用情况。 报告的值是针对所有测量时间间隔所计算的平均值。|
|规则类型|信息|

 使用采样法、.NET 内存或资源争用方法进行分析时，必须收集至少 10 个样本才能触发此规则。

## <a name="rule-description"></a>规则说明
 此消息用于报告此进程当前使用的平均物理内存字节数（工作集）。 进程工作集表示当前位于物理内存中的进程地址空间中的页面。

 报告的值包括进程已引用的共享内存段中的驻留页面。 进程引用的共享 DLL 包含在计算的共享内存段中。 受共享内存段的影响，进程工作集的值可能高于进程已经分配的虚拟内存量。

 报告的值是所分析的进程处于活动状态的所有测量时间间隔的平均值。

 进程工作集的大小反映进程当前使用的虚拟内存量。 它还受可用于运行应用程序的物理内存量（或 RAM）和其他运行的进程对该物理内存的争用量的影响。 如果物理内存受到约束，则进程工作集往往存在较大差别，因为操作系统将尝试从进程工作集通过定期修整活动程度相当低的进程，以平衡整个活动进程中的内存使用情况。

 有关进程工作集的详细信息，请参阅 MSDN 上 Windows 内存管理文档中的 [Working Set](/windows/win32/memory/working-set)（工作集）。

## <a name="how-to-use-rule-data"></a>如何使用规则数据
 若要了解不同分析方案中应用程序的性能，可使用规则值比较不同版本程序的性能。

 双击“错误列表”窗口中的消息，导航到分析数据的[标记视图](../profiling/marks-view.md)。 查找 **Process\Working Set** 和 **Memory\Pages/sec** 列。 比较两个列，并确定是否存在与增加的页面 IO 活动关联的特定阶段的程序执行。