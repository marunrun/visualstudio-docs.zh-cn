---
title: 筛选报告视图 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, configuring
ms.assetid: 820cf192-7fd6-4bee-9a51-aa69154aca85
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 344a2dbe0e629f62f609806008b963be2be058a1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68164055"
---
# <a name="filtering-report-views"></a>筛选报告视图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以将筛选器应用于分析数据文件，限制“性能报告”视图中显示的和导出到报告文件的分析数据。 可以将报告现定于两个时间戳值之间的数据，并可以将数据限定于特定的进程和线程。 可以将筛选器保存到文件，然后通过导入保存的筛选器，在另一分析数据文件中创建筛选器。  
  
 通过在“摘要”视图中使用图形时间线，还可以将报告限制到某一时间段。 请参阅[如何：从摘要时间线中筛选报告视图](../profiling/how-to-filter-report-views-from-the-summary-timeline.md)。  
  
 若要从报告中排除系统和第三方代码，请参阅[如何：筛选分析工具报告视图以显示“仅我的代码”](../profiling/how-to-filter-profiling-tools-report-views-to-display-just-my-code.md)  
  
## <a name="procedures"></a>过程  
  
#### <a name="to-create-a-profiler-report-filter"></a>创建探查器报告筛选器  
  
1. 如果未显示“性能报告”视图筛选器窗口，请单击“性能报告”视图工具栏上的“显示筛选器”  。  
  
     “性能报告”视图筛选器是一个表。 该表的每一行代表一个筛选器子句。 可以向筛选器添加任意多个子句。  
  
2. 对于要添加到筛选器的每个子句，在行的下列字段中，选择或输入值。  
  
    |字段|说明|  
    |-----------|-----------------|  
    |And/Or |如果此子句和下一个子句必须都为 true 才能匹配结果，则选择“与”  。 如果此子句或下一个子句为 true 即可匹配结果，则选择“或”  。|  
    |**字段**|从显示的数据字段列表中选择要在筛选器子句中使用的报告字段。|  
    |**Operator**|选择用于指定子句中字段与值之间的关系的运算符。<br /><br /> =    等于<br /><br /> <>  不等于<br /><br /> <    小于<br /><br /> >    大于<br /><br /> <=  小于或等于<br /><br /> >=  大于或等于|  
    |**值**|选择或输入要查找的值。 某些字段会列出字段的可用值。|  
  
3. 
  
#### <a name="to-create-a-profiler-report-filter-from-the-marks-report-view"></a>从“标记报告”视图中创建探查器报告筛选器  
  
1. 在“性能报告”视图工具栏上，从“当前视图”  列表中选择“标记”  。  
  
    此时将显示“标记探查器”报告。  
  
2. 选择要用作报告起始点的 ETW 或采样事件。  
  
3. 按住 Ctrl 并单击要用作报告结束点的事件。  
  
4. 右键单击，然后单击下列选项之一：  
  
   -  “添加针对标记的筛选器”将创建使用“标记”列作为筛选器字段的筛选器子句。  
  
   -  “添加针对时间戳的筛选器”将创建使用“时间戳(毫秒)”列作为筛选器字段的筛选器子句。  
  
     这两个选项在相同的开始点和结束点筛选当前数据文件。 如果将筛选器导出以供在其他报告中使用，可以选用任一选项。  
  
#### <a name="to-load-an-existing-filter-from-a-file"></a>从文件加载现有筛选器  
  
1. 在“性能报告视图”工具栏上，单击“导入筛选器”  。  
  
     此时将显示  “加载筛选器”对话框。  
  
2. 指定要加载的筛选器 (.vspf) 文件的位置和文件名。  
  
#### <a name="to-execute-a-filter"></a>执行筛选器  
  
- 在“性能报告视图”工具栏上，单击“执行筛选器”  。  
  
#### <a name="to-stop-a-filter-that-is-taking-too-long-to-execute"></a>停止耗费太长执行时间的筛选器  
  
- 在“性能报告视图”工具栏上，单击“停止筛选器”  。  
  
#### <a name="to-remove-a-filter-on-a-report-view"></a>删除报表视图中的筛选器  
  
1. 删除“性能报告视图”筛选器中的子句行。  
  
2. 在“性能报告视图”工具栏上，单击“执行筛选器”  。  
  
#### <a name="to-save-a-filter-to-a-file"></a>将筛选器保存到文件  
  
1. 在“性能报告视图”工具栏上，单击“导出筛选器”  。  
  
     此时将显示  “保存筛选器”对话框。  
  
2. 指定要保存的筛选器 (.vspf) 文件的位置和文件名。  
  
## <a name="see-also"></a>另请参阅  
 [自定义性能工具报表视图](../profiling/customizing-performance-tools-report-views.md)
