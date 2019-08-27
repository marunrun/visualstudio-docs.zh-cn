---
title: DA0026：处理过程的内核 CPU 时间过长 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.rules.DA0026
- vs.performance.DA0026
- vs.performance.26
ms.assetid: 4cfc8a29-b29b-4a72-b386-03d8856fdf8a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 906d24513982917a455fb7fc59940446c89dae45
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62936379"
---
# <a name="da0026-excessive-kernel-cpu-time-processing"></a>DA0026：处理过程的内核 CPU 时间过长

|||
|-|-|
|规则 ID|TODO|
|类别|分析工具使用情况|
|分析方法|采样|
|消息|测量相对较高的内核模式 CPU 时间量。 请考虑调查启用 SysCall 采样的源。|
|规则类型|信息|

 使用采样法、.NET 内存或资源争用方法进行分析时，必须收集至少 10 个样本才能触发此规则。

## <a name="cause"></a>原因
 内核模式下执行的 CPU 时间比例超过在用户模式下所花费的时间。 请考虑重新进行分析并对系统调用 (syscalls) 的数量进行采样，确定内核模式执行次数较多的原因。

## <a name="rule-description"></a>规则说明
 应用程序在内核模式下花费的时间相对较多则可能需要进一步调查。 将用户模式应用程序转换到内核模式，执行 I/O 操作、等待线程或进程同步基元，或执行系统调用。 可调查应用程序执行的系统调用的类型，以及调查基于系统调用选择收集示例调用堆栈的选项时，哪些函数对系统调用负责。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要调查应用程序执行的系统调用的类型，可再次运行分析，并基于系统调用选择收集示例的选项。 请参阅[如何：选择采样事件](../profiling/how-to-choose-sampling-events.md)以了解详细信息（如果在 IDE 内部运行分析工具）。 如果通过命令行运行分析工具，请参阅分析工具命令行工具引用中 [VSPerfCmd](../profiling/vsperfcmd.md) 文章的采样间隔选项部分。