---
title: 性能报告视图筛选器 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, Profiler Report view filter
- Profiler Report View filter, profiling tools
ms.assetid: 35f89d86-4683-4db1-aa0c-ae0ce65fa524
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ae4c5281386cb43d4dddb55db8578aea7515dce1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62793976"
---
# <a name="performance-report-view-filter"></a>性能报告视图筛选器
“探查器报告视图筛选器”窗口位于“性能报告”窗口顶部。 如果看不到它，请单击“显示筛选器”按钮。

 可以修改每个筛选器子句以优化结果。 筛选生成器中提供了以下各列。

|筛选器项|说明|
|-----------------|-----------------|
|与/或|如果此子句和下一个子句必须都为 true 才能匹配结果，则选择“与”。 如果此子句或下一个子句为 true 即可匹配结果，则选择“或”。|
|字段|从当前报告文件中可用的数据字段列表中选择要在筛选器子句中使用的字段。|
|运算符|选择用于指定字段与值之间的所需关系的运算符。<br /><br /> =    等于<br /><br /> <>  不等于<br /><br /> <    小于<br /><br /> >    大于<br /><br /> <=  小于或等于<br /><br /> >=  大于或等于|
|值|选择或输入要查找的值。 某些字段会列出字段的可用值。|

 可以添加筛选器子句，直到认为筛选器可提供最佳结果。 单击“执行筛选器”可将筛选器应用于数据文件。

 从“标记”报告视图中，可以生成筛选器子句，以将报告视图中的数据限制为在两个标记之间收集的数据。 选择你要用于开始和结束报告数据的标记，然后右键单击并选择“添加针对标记的筛选器”或“添加针对时间戳的筛选器”。 这两个筛选器都可将当前数据文件中的数据限制到相同范围；“添加针对标记的筛选器”可以应用于其他 .vsp 文件。

 若要保存筛选器，请单击“性能报告”工具栏上的“导出筛选器”，然后为 .vspf 文件指定位置和文件名。 若要加载以前保存的筛选器，请单击“导入筛选器”并查找保存的筛选器文件。 筛选器文件还可以用于在安装了独立分析工具的计算机上筛选数据文件。 有关详细信息，请参阅 [VSPerfReport](../profiling/vsperfreport.md)。

## <a name="see-also"></a>请参阅
- [分析性能工具数据](../profiling/analyzing-performance-tools-data.md)
- [VSPerfReport](../profiling/vsperfreport.md)