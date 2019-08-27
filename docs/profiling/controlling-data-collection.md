---
title: 控制数据收集 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- advanced tasks for profiling tools
- profiling tools, advanced tasks
ms.assetid: e713ad63-b948-46f3-8db9-59b30922ebe5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 250ec5623a02f962a0d56d7f469ed37afee097ab
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62553274"
---
# <a name="control-data-collection"></a>控制数据收集
通过 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具可控制性能会话期间收集分析数据的时间，并指定分析的函数。 本节介绍如何从“性能资源管理器”和“数据收集控制”窗口启动和停止数据收集，以及如何限制要收集其分析数据的对象。

## <a name="common-tasks"></a>常见任务

|任务|相关内容|
|----------|---------------------|
|**启动和停止分析：** 可以在应用程序启动时开始分析应用程序，或者将探查器附加到已在运行的进程。 目标应用程序运行时，可以暂停和恢复数据收集。 通过关闭目标应用程序或将探查器从运行中的进程中拆离可结束分析会话。|-   [如何：启动和结束性能数据收集](../profiling/how-to-start-and-end-performance-data-collection.md)<br />-   [如何：在正在运行的进程中附加和拆离性能工具](../profiling/how-to-attach-and-detach-performance-tools-to-running-processes.md)<br />-   [如何：暂停和恢复性能数据收集](../profiling/how-to-pause-and-resume-performance-data-collection.md)|
|**配置检测分析以限制收集的数据：** 可以使用性能会话配置属性限制在使用检测方法的分析运行中收集的数据。 可以包括或排除特定的 .dll 文件、命名空间、类和函数。 此外，还可以排除不满足指定大小阈值的函数。|-   [如何：将检测限定为特定 DLL](../profiling/how-to-limit-instrumentation-to-specific-dlls.md)<br />-   [如何：将检测限定为特定函数](../profiling/how-to-limit-instrumentation-to-specific-functions.md)<br />-   [如何：在检测中排除或包括短函数](../profiling/how-to-exclude-or-include-short-functions-from-instrumentation.md)|

## <a name="related-sections"></a>相关章节
- [配置性能会话](../profiling/configuring-performance-sessions.md)

## <a name="see-also"></a>请参阅
- [性能资源管理器](../profiling/performance-explorer.md)