---
title: DA0014：以分页方式将活动内存移到磁盘的发生率极高 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.rules.DAMemoryBound
- vs.performance.DA0014
- vs.performance.14
- vs.performance.rules.DA0014
ms.assetid: a7fa3749-9191-437a-9331-9d917181e62f
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: dbf391f96cd21f0c473589d4992083963ff65d55
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440918"
---
# <a name="da0014-extremely-high-rates-of-paging-active-memory-to-disk"></a>DA0014：以分页方式将活动内存移到磁盘的发生率极高
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

规则 Id |DA0014 |  
|类别 |内存和分页 |  
|分析方法 |所有 |  
|消息 |发生了极高比率的分页活动内存到磁盘。 应用程序可能受内存限制。|  
|规则类型 |警告 |  
  
 使用采样法、.NET 内存或资源争用方法进行分析时，必须至少收集 25 个样本才能触发此规则。  
  
## <a name="cause"></a>原因  
 在分析运行中收集的系统性能数据表明：在整个分析运行期间，到\来自磁盘的活动内存的分页速率极高。 此级别的分页速率通常会影响应用程序性能和响应能力。 请考虑通过修改算法来减少内存分配。 可能还需要考虑应用程序的内存要求。 在具有更多内存的计算机上再次运行分析。  
  
## <a name="rule-description"></a>规则说明  
 物理内存不足可能引起到磁盘的过度分页。 如果分页操作控制对分页文件所在物理磁盘的使用，它们将减缓对同一磁盘的其他面向应用程序的磁盘操作。  
  
 通常以批量分页操作从磁盘中读取页面或将页面写入磁盘。 例如，页面输出数/秒通常比页面写入数/秒大得多。 因为每秒页面输出还包括系统文件缓存中已更改的数据页面。 但是，确定哪个进程直接对分页负责及原因并不简单。  
  
> [!NOTE]
> 活动内存的分页级别达到较高速率时将会触发此规则。 当分页的级别较高但并非极高时，将改为触发 [DA0017：以分页方式将活动内存移到磁盘的发生率高](../profiling/da0017-high-rates-of-paging-active-memory-to-disk.md)信息规则。  
  
## <a name="how-to-fix-violations"></a>如何解决冲突  
 双击“错误列表”窗口中的消息，导航到[标记](../profiling/marks-view.md)视图。 查找 **Memory\Pages/sec** 列。 确定程序执行中是否存在分页 IO 活动要多于其他活动的某个阶段。  
  
 如果要在负载测试方案中收集 ASP.NET 应用程序的分析数据，请尝试在使用其他物理内存（或 RAM）配置的计算机上再次运行负载测试。  
  
 请考虑通过修改算法和避免使用占用大量内存的 API（如 String.Concat 和 String.Substring）来减少内存分配。
