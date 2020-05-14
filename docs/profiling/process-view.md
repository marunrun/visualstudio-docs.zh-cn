---
title: “进程”视图 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.process
helpviewer_keywords:
- performance tools reports, process view
- Process view
- performance tools, process view
- Profiling Tools,process view
- Profiling Tools,process report
ms.assetid: 6d4e2a5d-9f17-4ece-a6f1-75836e1fc382
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: da3097c276557238e6f5b521f6f7d3231434cd10
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74772171"
---
# <a name="process-view"></a>“进程”视图
“进程”视图显示在分析运行期间执行的进程和线程的分析数据。

 进程按名称列出。 线程作为创建它们的进程的子节点列出。 如果无可用符号，可以通过启动线程的函数或标签 **[ntdll.dll]** 对线程命名。

 若要添加和移除列，请右键单击视图，然后选择“添加/移除列”  。 此外，还可通过单击列名对数据进行排序。 有关详细信息，请参阅[如何：自定义报告视图列](../profiling/how-to-customize-report-view-columns.md)。

 对于使用采样和检测方法生成的数据和其中包含 .NET 内存数据的数据而言，“进程”视图的列相同。 下表对列值进行了说明。

|列|说明|
|------------|-----------------|
|**唯一 ID**|探查器生成的标识符，对进程或线程是唯一的。|
|**ID**|进程或线程的系统生成标识符。|
|**Name**|进程或线程的名称。|
|**开始时间**|从分析开始到进程或线程启动的毫秒数或处理器周期数。|
|**结束时间**|从分析开始到进程或线程结束的毫秒数或处理器周期数。|

## <a name="see-also"></a>另请参阅
- [采样方法数据视图](../profiling/profiler-sampling-method-data-views.md)
- [检测方法数据视图](../profiling/instrumentation-method-data-views.md)
- [.NET 内存数据视图](../profiling/dotnet-memory-data-views.md)
