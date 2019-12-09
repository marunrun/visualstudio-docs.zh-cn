---
title: DA0017：以分页方式将活动内存移到磁盘的发生率高 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.17
- vs.performance.rules.DA0017
- vs.performance.DA0017
ms.assetid: 01011eec-5930-43b3-980d-2cb01e2ca7f6
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 87e7c6b2d94602eca9e81098bb50bd0330b2bcd9
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74779384"
---
# <a name="da0017-high-rates-of-paging-active-memory-to-disk"></a>DA0017：以分页方式将活动内存移到磁盘的发生率高

|||
|-|-|
|规则 ID|DA0017|
|类别|内存和分页|
|分析方法|全部|
|消息|当前活动内存到磁盘的分页速率很高。 应用程序可能受内存限制。|
|规则类型|信息|

 使用采样法、.NET 内存或资源争用方法进行分析时，必须收集至少 10 个样本才能触发此规则。

## <a name="cause"></a>原因
 在分析运行中收集的系统性能数据表明：在整个分析运行期间，活动内存到磁盘的分页速率或从磁盘中分页活动内容的速率较高。 此级别的分页速率通常会影响应用程序性能和响应能力。 请考虑通过修改算法来减少内存分配。 可能还需要考虑应用程序的内存要求。

## <a name="rule-description"></a>规则说明

> [!NOTE]
> 当活动内存的分页级别达到较高级别时，将会触发此信息规则。 当分页级别极高时，将改为触发警告规则 [DA0014：活动内存到磁盘的分页速率极高](../profiling/da0014-extremely-high-rates-of-paging-active-memory-to-disk.md)。

 物理内存不足可能引起到磁盘的过度分页。 如果分页操作控制对分页文件所在物理磁盘的使用，它们将减缓对同一磁盘的其他面向应用程序的磁盘操作。

 通常以批量分页操作从磁盘中读取页面或将页面写入磁盘。 例如，每秒页面输出数通常比每秒页面写入数要大得多。 因为每秒页面输出还包括系统文件缓存中已更改的数据页面。 但是，确定哪个进程直接对分页负责及原因并不简单。

## <a name="how-to-fix-violations"></a>如何解决冲突
 双击“错误列表”窗口中的消息，导航到[标记](../profiling/marks-view.md)视图。 查找 **Memory\Pages/sec** 列。 确定程序执行中是否存在分页 IO 活动要多于其他活动的某个阶段。

 如果要在负载测试方案中收集 ASP.NET 应用程序的分析数据，请尝试在使用其他物理内存（或 RAM）配置的计算机上再次运行负载测试。

 请考虑通过修改算法和避免使用占用大量内存的 API（如 String.Concat 和 String.Substring）来减少内存分配。
