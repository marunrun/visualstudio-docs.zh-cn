---
title: 分析 .NET 对象的内存使用情况 | Microsoft Docs
ms.date: 12/9/2019
ms.topic: conceptual
helpviewer_keywords:
- memory allocation, memory usage
author: Sagar-S-S
ms.author: sashe
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: 2a812ea3dcddc2fa6093b2b5b99684d1d5194654
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85279989"
---
# <a name="analyze-memory-usage-by-using-the-net-object-allocation-tool"></a>使用 .NET 对象分配工具分析内存使用情况

可以使用 .NET 对象分配工具来了解应用使用了多少内存，以及哪些代码路径分配了最多的内存。

运行此工具后，可以查看要在其中分配对象的函数执行路径。 然后，可以追溯到占用内存最多的调用树的根。

## <a name="setup"></a>安装

1. 在 Visual Studio 中，按 Alt+F2 打开性能探查器。

1. 选中“.NET 对象分配跟踪”复选框。

   ![已选中“.NET 对象分配跟踪”工具](../profiling/media/dotnetalloctoolselected.png "已选中“.NET 对象分配跟踪”工具")

1. 选择“开始”按钮，以运行此工具。

1. 在此工具开始运行后，在应用中完成要探查的方案。 然后，选择“停止收集”或关闭应用，以查看数据。

   ![显示“停止收集”的窗口](../profiling/media/stopcollectionlighttheme.png "显示“停止收集”的窗口")

1. 选择“分配”选项卡。此时，类似于以下屏幕截图的窗口内容显示。

   ![“分配”选项卡](../profiling/media/allocationview.png "“分配”选项卡")

你现可分析对象的内存分配情况了。

在收集过程中，跟踪工具可能会减慢被探查的应用的速度。 如果跟踪工具或应用的性能较慢，并且你不需要跟踪每个对象，则可以调整采样率。 为此，请在“探查器摘要”页中选择跟踪工具旁边的齿轮符号。

![.NET 分配工具的设置](../profiling/media/dotnetallocsettings.png ".NET 分配工具的设置")

将采样率调整为所需的值。 此更改有助于在收集和分析期间让应用的性能提速。

![调整后的采样率](../profiling/media/adjustedsamplingratedotnetalloctool.png "调整后的采样率")

若要详细了解如何提高此工具的效率，请参阅[优化探查器设置](../profiling/optimize-profiler-settings.md)。

## <a name="understand-your-data"></a>了解数据

![.NET 分配工具图](../profiling/media/graphdotnetalloc.png ".NET 分配工具图")

在上面的图形视图中，最上面的图显示了应用中的活动对象数。 最下面的“对象增量”图显示了应用对象数变化率 (%)。 红色条表示垃圾回收的发生时间。

![筛选时间后的 .NET 分配图](../profiling/media/graphdotnetalloctimefiltered.png "筛选时间后的 .NET 分配图")

可以筛选表格数据，只显示指定时间范围内的活动。 还可以放大或缩小此图。

### <a name="allocation"></a>分配

![展开的“分配”视图](../profiling/media/allocationexpandedlight.png "展开的“分配”视图")

“分配”视图显示了正在分配内存的对象的位置，以及这些对象正在分配的内存量。

- “类型” **** 列是占用内存的类和结构的列表。  双击某一类型，以倒调用树的形式查看其回溯。 仅在“分配”视图中，可以看到所选类别中占用内存的项。

- “分配” **** 列显示了特定分配类型或函数内占用内存的对象数。  此列仅在“分配”、“调用树” **** 和“函数” **** 视图中显示。 

- 默认情况下，“字节” **** 和“平均大小(字节)” **** 列不显示。   若要显示这些列，请右键单击“类型” **** 或“分配” **** 列，然后选择“字节”和“平均大小(字节)” **** 选项，以将这些列添加到图表中。     

   这两列类似于“总计(分配)” **** 和“自身(分配)” **** ，区别在于它们显示占用的内存量，而不是占用内存的对象数。 这些列仅在“分配”视图中显示。

- “模块名称” **** 列显示了包含正在调用模块的函数或进程的模块。 

所有这些列都是可排序的。 对于“类型” **** 和“模块名称”列，可以按字母顺序对项进行升序或降序排序。 对于“分配” **** 、“字节”和“平均大小(字节)” **** ，可以通过增加或减少数值来对项进行排序。 

#### <a name="symbols"></a>符号

以下符号在“分配”、“调用树”和“函数”选项卡中显示：

- ![值类型符号](../profiling/media/valuetypeicon.png "值类型符号") - 值类型（如整数）

- ![值类型集合符号](../profiling/media/valuetypecollectionicon.png "值类型集合符号") - 值类型集合（如整数数组）

- ![引用类型符号](../profiling/media/referencetypeicon.png "引用类型符号") - 引用类型（如字符串）

- ![引用类型集合符号](../profiling/media/referencetypecollectionicon.png "引用类型集合符号") - 引用类型集合（如字符串数组）

### <a name="call-tree"></a>调用树

![“调用树”视图](../profiling/media/calltreelight.png "“调用树”视图")

“调用树” **** 视图显示了包含分配大量内存的对象的函数执行路径。 

- “函数名称” **** 列显示了包含分配内存的对象的进程或函数名称。  显示内容因要检查的节点级别而异。
- “总计(分配)” **** 和“总大小(字节)” **** 列显示了已分配的对象数，以及函数及其调用的其他所有函数使用的内存量。 
- “自身(分配)”和“自大小(字节)”列显示了已分配的对象数，以及所选的一个函数或分配类型使用的内存量。
- “平均大小(字节)”列显示的信息与“分配”视图中显示的信息相同。
- “模块名称” **** 列显示了包含正在调用模块的函数或进程的模块。 

   ![展开的热路径](../profiling/media/hotpathlight.png "展开的热路径")

- “展开热路径”按钮突出显示了包含许多正在分配内存的对象的函数执行路径。 此算法从你选择的节点开始，并突出显示分配最多的路径，从而指导你进行调查。
- “显示热路径”按钮可显示或隐藏火焰符号，这些符号表示哪些节点是热路径的一部分。

### <a name="functions"></a>函数

![“函数”视图](../profiling/media/functionslight.png "“函数”视图")

“函数”视图显示了正在分配内存的进程、模块和函数。

- “名称”列将进程显示为最高级别的节点。 进程下面是模块，模块下面是函数。
- 下面这些列显示的信息与“分配”和“调用树”视图中显示的信息相同：

   - **总计(分配)**
   - **自身(分配)**
   - **总大小(字节)**
   - **自大小(字节)**
   - **平均大小(字节)**

### <a name="collection"></a>集合

![“收集”视图](../profiling/media/collectionlight.png "“收集”视图")

“收集”视图显示了在垃圾回收期间收集或保留的对象数。 此视图还显示饼图，以按类型直观显示收集和保留的对象。

- “已收集”列显示了垃圾回收器收集的对象数。
- “已保留”列显示了运行垃圾回收器后保留的对象数。

### <a name="filtering-tools"></a>筛选工具

“分配”、“调用树”和“函数”视图都包含“仅显示我的代码”和“显示本机代码”选项，以及一个筛选器框。

- “仅显示我的代码”将系统、框架和其他非用户代码折叠为“[外部代码]”框架，这样你就可以专注于自己的代码。 有关详细信息，请参阅[使用“仅我的代码”调试用户代码](../debugger/just-my-code.md)。
- “显示本机代码”显示分析目标中的本机代码，可以包括非用户代码。
- 通过筛选器框，可根据你提供的值来筛选“名称”或“函数名称”列。 在框中输入字符串值。 然后，表中只显示包含此字符串的类型。
