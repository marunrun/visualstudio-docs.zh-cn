---
title: 分析不调试的内存使用情况 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 16b46d47ec5850a79d78667671c7eb671d859f3e
ms.sourcegitcommit: 53bc4c11b82882ab658e34c65ae374060f823531
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2019
ms.locfileid: "71128238"
---
# <a name="analyze-memory-usage-without-the-debugger"></a>分析不调试的内存使用情况

“内存使用情况”工具监视应用的内存使用情况  。 可以使用该工具来研究在 Visual Studio 中正在积极开发的场景的实时内存效果。 可以获取应用内存状态的详细情况快照，并比较快照以找出内存问题的根本原因。

“内存使用情况”工具在带或不带调试器的情况下都可以运行  。 以下说明介绍如何在 Visual Studio“性能探查器”中使用不带调试器的“内存使用情况”工具   。

>[!NOTE]
>- 要测量 .NET Core 应用的内存使用情况，必须将“内存使用情况”工具与调试器一起使用  。 有关说明，请参阅 [Visual Studio 中的配置文件内存使用情况](memory-usage.md)。
>- 要分析 JavaScript 或 HTML UWP 应用中的内存使用情况，请使用性能探查器中的 [JavaScript 内存](../profiling/javascript-memory.md)工具  。

## <a name="memory-usage-diagnostic-sessions"></a>内存使用情况诊断会话

**启动内存使用情况诊断对话：**

1. 请在 Visual Studio 中打开 C# 通用 Windows 平台 (UWP) 项目。

1. 在菜单栏上，选择“调试”   > “性能探查器”  。

1. 选择“内存使用情况”，然后选择“启动”   。

   ![启动内存使用量诊断会话](../profiling/media/memuse_start_diagnosticssession.png "Start a Memory Usage diagnostic session")

### <a name="monitor-memory-use"></a>监视内存使用情况

启动诊断会话时，应用将启动，并且“诊断工具”窗口将显示此应用的内存使用情况的时间线图  。

![“内存使用率”概述页](../profiling/media/memuse__reportoverview.png "MEMUSE__ReportOverview")

时间线图显示应用运行时的内存波动情况。 该关系图中的峰值通常表明一些代码正在收集或创建数据，然后在处理完成后放弃它。 较大的峰值表明能够进行优化的区域。 更需关注的是未返回的内存消耗中出现增加，因为这可能表明低效的内存使用情况或甚至表明出现内存泄露。

### <a name="take-snapshots-of-app-memory-states"></a>拍摄应用内存状态的快照

应用使用大量对象，因此你可能希望集中分析某一种情况。 或者，可能会发现要调查的内存问题。 可以在诊断会话期间拍摄快照以捕获特定时刻的内存使用情况。 一个较好的办法是，获取应用在出现内存问题之前的基线快照、首次出现问题后的另一个快照，以及其他快照（如果可重复执行该方案）。

要收集快照，请在要捕获内存数据时选择“拍摄快照”  。

### <a name="BKMK_Close_a_monitoring_session"></a> 关闭诊断会话

若要在不创建报告的情况下监视会话，只需关闭诊断窗口。 要在完成收集或拍摄快照后生成报表，请选择“停止收集”  。

![停止收集](../profiling/media/memuse__stopcollection.png "Stop Collection")

## <a name="memory-usage-reports"></a>内存使用情况报表

停止收集数据后，“内存使用情况”工具将停止应用并显示“内存使用情况”概述页   。

![内存使用情况概述页](../profiling/media/memuse__reportoverview1.png "Memory Usage overview page")

### <a name="BKMK_Memory_Usage_snapshot_views"></a> 内存使用情况快照

“快照”窗格中的数字显示每个快照拍摄时内存中的字节和对象，以及快照和上一个快照之间的差异  。

这些数字是打开新 Visual Studio 窗口中详细的“内存使用情况”报表视图的链接  。 [快照详细报表](#snapshot-details-reports)显示了某个快照中的类型和实例。 [快照差异报表](#snapshot-difference-diff-reports)会比较两个快照中的类型和实例。

  ![快照视图链接](../profiling/media/memuse__snapshotview_numbered.png "Snapshot view links")

|||
|-|-|
|![第 1 步](../profiling/media/procguid_1.png "ProcGuid_1")|拍摄快照时内存中的字节总数。<br /><br /> 选择此链接以显示快照详细信息报表，该报表按类型实例的总大小进行排序。|
|![第 2 步](../profiling/media/procguid_2.png "ProcGuid_2")|拍摄快照时内存中的对象总数。<br /><br /> 选择此链接以显示快照详细信息报表，该报表按类型实例的计数进行排序。|
|![第 3 步](../profiling/media/procguid_3.png "ProcGuid_3")|此快照中内存对象的总大小与前一个快照之间的差异。 <br /><br /> 正数表示此快照的内存大于前一个快照，负数表示该快照的内存小于前一个快照。 “基线”表示快照是诊断会话中的第一个快照  。 “无差异”表示差异为零  。<br /><br /> 选择此链接以显示快照差异报表，该报表按类型实例的总大小的差异进行排序。|
|![第 4 步](../profiling/media/procguid_4.png "ProcGuid_4")|此快照中内存对象的总数与前一个快照之间的差异。<br /><br /> 选择此链接以显示快照差异报表，该报表按类型实例总数的差异进行排序。|

## <a name="memory-usage-snapshot-reports"></a>内存使用情况快照报表

<a name="BKMK_Snapshot_report_trees"></a> 当在“内存使用情况”概述页中选择某个快照链接时，快照报表将在新页面中打开  。

![内存使用情况快照报表](../profiling/media/memuse_snapshotreport_all.png "Memory Usage snapshot report")

在快照报表中，可展开“对象类型”条目以显示子项  。 实例名是由内存使用量工具生成的唯一 ID。

如果“对象类型”是蓝色，则可以在单独的窗口中选择它以导航到源代码中的对象  。

无法识别或无法理解的代码中涉及的类型可能是 .NET Framework、操作系统或编译器对象。 如果这些对象涉及对象的所有权链，则“内存使用情况”工具会显示这些对象  。

在快照报表中：

- “托管堆”树在报表中显示类型和实例  。 通过选择类型或实例，可以显示选定项的**根路径**和**引用的对象**树。

- “根的路径”树显示引用类型或实例的对象链  。 .NET Framework 垃圾回收器仅在释放对某个对象的所有引用后清理该对象的内存。

- “引用类型”或“引用对象”树显示所选类型或实例引用的对象   。

### <a name="BKMK_Report_tree_filters_"></a>报告树筛选器

应用中的许多类型对应用程序开发人员来说并不是很有趣。 快照报表筛选器可以将大多数这些类型隐藏在“托管堆”和“根的路径”树的路径中   。

![排序和筛选选项](../profiling/media/memuse_sortandfilter.png "MEMUSE_SortAndFilter")

- <a name="BKMK_Filter"></a> 要按类型名称筛选树，请在“筛选器”框中输入名称  。 筛选器不区分大小写，并且可识别类型名称任意部分中指定的字符串。

- <a name="BKMK_Collapse_Small_Objects"></a> 在“筛选器”下拉列表中选择“隐藏小型对象”以隐藏以隐藏其大小（字节）小于内存总数 0.5% 的类型    。

- <a name="BKMK_Just_My_Code"></a> 在“筛选器”下拉列表中选择“仅我的代码”，以隐藏由外部代码生成的大多数实例   。 外部类型属于操作系统或 Framework 组件，或者由编译器生成。

## <a name="snapshot-details-reports"></a>快照详细信息报告

 快照详细信息报表描述诊断会话中的一个快照。 要打开此报表，请选择快照窗格中的大小或对象链接。

 ![链接到快照窗格中的快照报表](../profiling/media/memuse_snapshotview_snapshotdetailslinks.png "Links to snapshot report in a snapshot pane")

这两个链接都会打开同一个报表。 唯一的区别是“托管堆”树的起始排序顺序不同  。 大小链接按“非独占大小(字节)”列对报表进行排序  。 对象链接按“计数”列对报表进行排序  。 可以在报表打开后更改排序列或顺序。

### <a name="BKMK_Managed_Heap_tree__Snapshot_details_"></a>托管堆树（快照详细信息报表）
 **托管堆**树列出了内存中保存的对象类型。 可以展开类型名称以查看十大类型示例（按大小排列）。 通过选择类型或实例，以显示选定项的“根的路径”和“引用对象”树   。

 ![托管堆树](../profiling/media/memuse__snapshotdetails_managedheaptree.png "Managed Heap tree")

“托管堆”树在快照详细信息报表中包含以下列  ：

|||
|-|-|
|“对象类型” |类型或对象实例的名称。|
|“计数” |类型的对象实例数。 对于实例，“计数”始终为 1  。|
|“大小(字节)” |对于类型，快照中所有类型实例的大小都小于实例中包含的对象的大小。<br /><br /> 对于实例，对象的大小小于实例中包含的对象大小。 |
|“非独占大小(字节)” |类型实例的大小或单个实例的大小，其中包括所含对象的大小。|
|**模块**|包含此对象的模块。|

### <a name="BKMK_Paths_to_Root_tree__Snapshot_details_"></a> 根的路径树（快照详细信息报表）
“根的路径”树显示引用类型或实例的对象链  。 .NET Framework 垃圾回收器仅在释放对某个对象的所有引用后清理该对象的内存。

对于“根的路径”树中的类型，持有对该类型的引用的对象的数量将出现在“引用计数”列中   。

![各类型的根的路径树](../profiling/media/memuse_snapshotdetails_type_pathstoroottree.png "Paths to Root tree for types")

### <a name="BKMK_Referenced_Objects_tree__Snapshot_details_"></a> 引用类型或引用对象树（快照详细信息报表）
“引用类型”或“引用对象”树显示所选类型或实例引用的对象   。

![实例的引用对象树](../profiling/media/memuse_snapshotdetails_referencedobjects_instance.png "Referenced Objects tree for instances")

“引用类型”树在快照详细信息报表中包含以下列  ： “引用对象”树没有“引用计数”列   。

|||
|-|-|
|“对象类型”或“实例”  |类型或实例的名称。|
|**引用计数**|对于类型，该类型的对象实例数。|
|“大小(字节)” |对于类型，类型的所有实例的大小都小于类型中包含的对象的大小。<br /><br /> 例如，对象的大小小于对象中包含的对象的大小。|
|“非独占大小(字节)” |类型实例的总大小或实例的大小，其中包括所包含的对象的大小。|
|**模块**|包含此对象的模块。|

## <a name="snapshot-difference-diff-reports"></a>快照差异报告

快照差异（差异）报表显示主快照和前一个快照之间的更改。 要打开差异报表，请在快照窗格中选择差异链接。

这两个链接都会打开同一个报表。 唯一的区别是报表中“托管堆”树的起始排序顺序不同  。 大小链接按“非独占大小差异(字节)”列对报表进行排序  。 对象链接按“计数差异”列对报表进行排序  。 可以在报表打开后更改排序列或顺序。

 ![快照窗格中的差异报表链接](../profiling/media/memuse_snapshotview_snapshotdifflinks.png "Links to difference report in a snapshot pane")

### <a name="BKMK_Managed_Heap_tree__Snapshot_diff_"></a>托管堆树（快照差异报表）

 **托管堆**树列出了内存中保存的对象类型。 你可以展开类型名称以查看十大类型示例（按大小排列）。 通过选择类型或实例，以显示选定项的“根的路径”和“引用对象”树   。

 ![差异报表中的类型的托管堆树](../profiling/media/memuse_snapshotdiff_type_heap.png "Managed Heap tree for a type in difference report")

“托管堆”树在快照差异报表中包含以下列  ：

|||
|-|-|
|“对象类型” |类型或对象实例的名称。|
|“计数” |主要快照中的类型实例的数量。 对于实例，“计数”  始终为 1。|
|“计数差异” |对于类型，则为主要快照与上一个快照之间的类型实例数的差异。 对于实例，字段是空白的。|
|“大小(字节)” |主快照中对象的大小小于对象中包含的对象的大小。 对于类型，“大小(字节)”  和“非独占大小(字节)”  为类型实例的总大小。|
|“总大小差异(字节)” |对于类型，主快照和上一个快照之间的类型实例总大小的差异小于实例中包含的对象的大小。 对于实例，字段是空白的。|
|“非独占大小(字节)” |主要快照中对象的大小，其中包括对象中包含的对象的大小。|
|“非独占大小差异(字节)” |对于类型，主快照和上一个快照之间的所有类型实例大小的差异，其中包括对象中包含的对象的大小。 对于实例，字段是空白的。|
|**模块**|包含此对象的模块。|

### <a name="BKMK_Paths_to_Root_tree__Snapshot_diff_"></a> 根的路径树（快照差异报表）

“根的路径”树显示引用类型或实例的对象链  。 .NET Framework 垃圾回收器仅在释放对某个对象的所有引用后清理该对象的内存。

对于“根的路径”树中的类型，持有对该类型的引用的对象的数量将出现在“引用计数”列中   。 上一个快照的差异计数显示在“引用差异”列  。

 ![差异报表中的根的路径树](../profiling/media/memuse_snapshotdiff_pathstoroot_instance_all.png "Paths To Root tree in a diff report")

### <a name="BKMK_Referenced_Objects_tree__Snapshot_diff_"></a> 引用类型或引用对象树（快照差异报表）

“引用类型”或“引用对象”树显示所选类型或实例引用的对象   。

![差异报表中的引用类型](../profiling/media/memuse_snapshotdiff_referencedtypes.png "Referenced Types in a diff report")

“引用类型”树在快照差异报表中包含以下列  ： “引用对象”树有“实例”大小（字节）、非独占大小（字节）和“模块”列      。

|||
|-|-|
|“对象类型”或“实例”  |类型或对象实例的名称。|
|**引用计数**|主要快照中的类型实例的数量。|
|**引用计数差异**|对于类型，则为主要快照与上一个快照之间的类型实例数的差异。|
|“大小(字节)” |主快照中对象的大小小于对象中包含的对象的大小。 对于类型，“大小(字节)”  和“非独占大小(字节)”  为类型实例的总大小。|
|“总大小差异(字节)” |对于类型，主快照和上一个快照之间的类型实例总大小的差异小于实例中包含的对象的大小。 |
|“非独占大小(字节)” |主要快照中对象的大小，其中包括对象中包含的对象的大小。|
|“非独占大小差异(字节)” |对于类型，主快照和上一个快照之间的所有类型实例大小的差异，其中包括对象中包含的对象的大小。|
|**模块**|包含此对象的模块。|

## <a name="see-also"></a>请参阅
- [JavaScript 内存](../profiling/javascript-memory.md)
- [使用 Visual Studio 分析](../profiling/index.yml)
- [首先了解分析工具](../profiling/profiling-feature-tour.md)
- [使用 C++、C# 和 Visual Basic 的 UWP 应用的性能最佳做法](/previous-versions/windows/apps/hh750313\(v\=win.10\))
- [Diagnosing memory issues with the new Memory Usage Tool in Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=394706)（在 Visual Studio 中使用新的内存使用情况工具诊断内存问题）