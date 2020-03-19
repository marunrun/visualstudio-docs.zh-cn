---
title: DA0506：为所分析的进程分配的最大专用字节数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.rules.DA0506
- vs.performance.DA0506
- vs.performance.506
ms.assetid: e9c43554-9a85-4d98-9fa4-3b19986e7b62
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 7600e65beb3035fac6d5ea58b25f6965d681f83a
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74779306"
---
# <a name="da0506-maximum-private-bytes-allocated-for-the-process-being-profiled"></a>DA0506：为所分析的进程分配的最大专用字节数

|||
|-|-|
|规则 ID|DA0506|
|类别|资源监控|
|分析方法|All|
|消息|收集此信息仅用于参考。 进程专用字节计数器测量由正在分析的进程分配的虚拟内存。 报告的值是在所有测量时间间隔内观察到的最大值。|
|规则类型|信息|

 使用采样法、.NET 内存或资源争用方法进行分析时，必须收集至少 10 个样本才能触发此规则。

## <a name="rule-description"></a>规则说明
 此消息用于报告进程当前已分配的虚拟内存的最大字节数（专用字节）。 专用字节表示由进程分配的虚拟内存位置，只能通过进程内部运行的线程访问此进程。

 对于在 32 位计算机上运行的 32 位进程，进程地址空间专用部分的上限为 2 GB。 使用 [/3GB](https://support.microsoft.com/help/833721/available-switch-options-for-the-windows-xp-and-the-windows-server-200) Boot.ini 开关，32 位进程最多可以获得 3 GB 的虚拟内存。 在 64 位计算机上运行的 32 位进程最多可以获得 4 GB 的专用虚拟内存。

 在 64 位计算机上运行的 64 位进程最多可以获得 8 TB 的专用虚拟内存。

 报告的值是所分析的进程在其中处于活动状态的所有测量间隔的最大值。

 有关进程地址空间的详细信息，请参阅 Windows 内存管理文档中的 [Virtual Address Space](/windows/win32/memory/virtual-address-space)（虚拟地址空间）。

## <a name="how-to-use-rule-data"></a>如何使用规则数据
 若要了解不同分析方案中应用程序的性能，可使用报告的值比较不同版本程序的性能。

 如果进程专用字节的最大值即将达到进程地址空间可以增长到的体系结构大小限制，则可能导致内存不足的异常。 有关详细信息，请参阅 MSDN 杂志期刊中的[调查内存问题](https://msdn.microsoft.com/magazine/cc163528.aspx)。
