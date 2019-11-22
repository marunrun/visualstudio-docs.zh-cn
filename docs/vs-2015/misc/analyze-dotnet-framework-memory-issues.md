---
title: Analyze .NET Framework memory issues | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
f1_keywords:
- vs.diagnostics.managedmemoryanalysis
ms.assetid: 43341928-9930-48cf-a57f-ddcc3984b787
caps.latest.revision: 9
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e94edbeac381ac634171507766126ab954153eb1
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295895"
---
# <a name="analyze-net-framework-memory-issues"></a>分析 .NET Framework 内存问题
通过使用 Visual Studio 托管内存分析程序，在 .NET Framework 代码中查找内存泄漏和低效内存使用。 目标代码的最低 .NET Framework 版本为 .NET Framework 4.5。  
  
 The memory analysis tool analyzes information in *dump files with heap data* that a copy of the objects in an app's memory. 从 Visual Studio IDE 或通过使用其他系统工具，你可以收集转储 (.dmp) 文件。  
  
- 你可以分析单个快照以了解有关内存使用的对象类型的相对影响，并在你的应用中查找低效使用内存的代码。  
  
- You can also compare (*diff*) two snapshots of an app to find areas in your code that cause the memory use to increase over time.  
  
  For a walkthrough of the managed memory analyzer, see [Using Visual Studio 2013 to Diagnose .NET Memory Issues in Production](https://devblogs.microsoft.com/devops/using-visual-studio-2013-to-diagnose-net-memory-issues-in-production/) on the Visual Studio ALM + Team Foundation Server blog .  
  
## <a name="BKMK_Contents"></a> 内容  
 [Memory use in .NET Framework apps](#BKMK_Memory_use_in__NET_Framework_apps)  
  
 [Identify a memory issue in an app](#BKMK_Identify_a_memory_issue_in_an_app)  
  
 [Collect memory snapshots](#BKMK_Collect_memory_snapshots)  
  
 [Analyze memory use](#BKMK_Analyze_memory_use)  
  
## <a name="BKMK_Memory_use_in__NET_Framework_apps"></a> Memory use in .NET Framework apps  
 .NET Framework 为垃圾回收运行时，这样在大多数应用中，内存使用不会成为问题。 但在长时间运行的应用程序中（如 Web 服务和应用程序），以及在只有有限内存的设备中，对象在内存中的累积会影响应用以及运行应用的设备的性能。 如果垃圾回收器运行过于频繁，或者如果强制操作系统在 RAM 和磁盘之间移动内存，则过多占用内存会停止应用程序和资源所在的计算机。 在最坏情况下，应用会因“内存不足”异常而崩溃。  
  
 The .NET *managed heap* is a region of virtual memory where reference objects created by an app are stored. 对象的生存期由垃圾收集器 (GC) 管理。 垃圾收集器使用引用以跟踪占用内存块的对象。 当创建对象并将其分配到变量时，就会创建一个引用。 单个对象可以具有多个引用。 例如，对一个对象的其他引用可以通过将该对象添加到类、集合或其他数据结构来创建，也可以通过将该对象分配给第二个变量来创建。 创建引用的一个不太明显的方式是通过一个对象将处理程序添加到另一个对象的事件。 在这种情况下，第二个对象保留对第一个对象的引用，直到该处理程序被显式删除或第二个对象被销毁。  
  
 对于每个应用程序，GC 维护跟踪由应用程序所引用的对象的引用树。 The *reference tree* has a set of roots, which includes global and static objects, as well as associated thread stacks and dynamically instantiated objects. 如果一个对象具有至少一个保存对其引用的父对象，则该对象为根对象。 只有当应用程序中的其他对象或变量都不具有对它的引用时，GC 才能回收对象的内存。  
  
 ![Back to top](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Contents](#BKMK_Contents)  
  
## <a name="BKMK_Identify_a_memory_issue_in_an_app"></a> Identify a memory issue in an app  
 内存问题的最明显症状是应用的性能，尤其是如果随着时间的推移性能降低。 当你的应用运行时，其他应用的性能下降，也可能表示存在内存问题。 If you suspect a memory issue, use a tool like Task Manager or [Windows Performance Monitor](https://technet.microsoft.com/library/cc749249.aspx) to investigate further. 例如，查看无法解释为内存泄漏可能来源的内存总大小的增长：  
  
 ![Consistent memory growth in Resource Monitor](../misc/media/mngdmem-resourcemanagerconsistentgrowth.png "MNGDMEM_ResourceManagerConsistentGrowth")  
  
 你可能还会注意到内存峰值，它们比就你所知的代码建议的值大，可能指向某个过程内的低效内存使用：  
  
 ![Memory spikes in Resource Manager](../misc/media/mngdmem-resourcemanagerspikes.png "MNGDMEM_ResourceManagerSpikes")  
  
## <a name="BKMK_Collect_memory_snapshots"></a> Collect memory snapshots  
 The memory analysis tool analyzes information in *dump files* that contain heap information. You can create dump files in Visual Studio, or you can use a tool like [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx) from [Windows Sysinternals](https://technet.microsoft.com/sysinternals). See [What is a dump, and how do I create one?](https://blogs.msdn.microsoft.com/debugger/2009/12/30/what-is-a-dump-and-how-do-i-create-one/) on the Visual Studio Debugger Team blog.  
  
> [!NOTE]
> 大部分工具可以收集附带或不附带完整堆内存数据的转储信息。 Visual Studio 内存分析程序需要完整的堆信息。  
  
 **To collect a dump from Visual Studio**  
  
1. 你可以针对从 Visual Studio 项目开始的进程创建一个转储文件，或者也可以将调试器附加到正在运行的进程。 See [Attach to Running Processes](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).  
  
2. 停止执行。 The debugger stops when you choose **Break All** on the **Debug** menu, or at an exception or at a breakpoint  
  
3. On the **Debug** menu, choose **Save Dump As**. In the **Save Dump As** dialog box, specify a location and make sure that **Minidump with Heap** (the default) is selected in the **Save as type** list.  
  
   **To compare two memory snapshots**  
  
   若要分析应用内存使用中的增长，请从该应用的单个实例收集两个转储文件。  
  
   ![Back to top](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Contents](#BKMK_Contents)  
  
## <a name="BKMK_Analyze_memory_use"></a> Analyze memory use  
 [Filter the list of objects](#BKMK_Filter_the_list_of_objects) **&#124;** [Analyze memory data in from a single snapshot](#BKMK_Analyze_memory_data_in_from_a_single_snapshot) **&#124;** [Compare two memory snapshots](#BKMK_Compare_two_memory_snapshots)  
  
 若要针对内存使用问题分析转储文件：  
  
1. In Visual Studio, choose **File**, **Open** and specify the dump file.  
  
2. On the **Minidump File Summary** page, choose **Debug Managed Memory**.  
  
    ![Dump file summary page](../misc/media/mngdmem-dumpfilesummary.png "MNGDMEM_DumpFileSummary")  
  
   内存分析程序启动调试会话以分析文件并且在“堆视图”页面上显示结果：  
  
   ![Back to top](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Contents](#BKMK_Contents)  
  
### <a name="BKMK_Filter_the_list_of_objects"></a> Filter the list of objects  
 默认情况下，内存分析程序在内存快照中筛选对象列表，以便只显示用户代码的类型和实例，并且只显示那些总包含大小超过总堆大小阈值百分比的类型。 You can change these options in the **View Settings** list:  
  
|||  
|-|-|  
|**启用“仅我的代码”**|“仅我的代码”将隐藏最常用的系统对象，以便只有你创建的类型显示在列表中。<br /><br /> You can also set the Just My Code option in the Visual Studio **Options** dialog box. 在 **“调试”** 菜单上，选择 **“选项和设置”** 。 In the **Debugging**/**General** tab, choose or clear **Just My Code**.|  
|**Collapse Small Objects**|**Collapse Small Objects** hides all types whose total inclusive size is less than 0.5 percent of the total heap size.|  
  
 You can also filter the type list by entering a string in the **Search** box. 该列表只显示那些名称中包含字符串的类型。  
  
 ![Back to top](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Contents](#BKMK_Contents)  
  
### <a name="BKMK_Analyze_memory_data_in_from_a_single_snapshot"></a> Analyze memory data in from a single snapshot  
 Visual Studio 启动新的调试会话以分析文件，并且在“堆视图”窗口中显示内存数据。  
  
 ![The Object Type list](../misc/media/dbg-mma-objecttypelist.png "DBG_MMA_ObjectTypeList")  
  
 ![Back to top](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Contents](#BKMK_Contents)  
  
#### <a name="object-type-table"></a>对象类型表  
 上表列出了在内存中保留的对象的类型。  
  
- **Count** shows the number of instances of the type in the snapshot.  
  
- **Size (Bytes)** is the size of the all instances of the type, excluding the size of objects it holds references to. 必须向  
  
- **Inclusive Size (Bytes)** includes the sizes of referenced objects.  
  
  You can choose the instances icon (![The instance icon in the Object Type column](../misc/media/dbg-mma-instancesicon.png "DBG_MMA_InstancesIcon")) in the **Object Type** column to view a list of the instances of the type.  
  
#### <a name="instance-table"></a>实例表  
 ![Instances table](../misc/media/dbg-mma-instancestable.png "DBG_MMA_InstancesTable")  
  
- **Instance** is the memory location of the object that serves as the object identifier of the object  
  
- **Value** shows the actual value of value types. 你可以悬停在引用类型的名称上以便在数据提示中查看其数据值。  
  
   ![Instance values in a data tip](../misc/media/dbg-mma-instancevaluesindatatip.png "DBG_MMA_InstanceValuesInDataTip")  
  
- **Size (Bytes)** is the size of the object, excluding the size of objects it holds references to. 必须向  
  
- **Inclusive Size (Bytes)** includes the sizes of referenced objects.  
  
  By default, types and instances are sorted by **Inclusive Size (Bytes)** . 在列表中选择一个列标题以更改排序顺序。  
  
#### <a name="paths-to-root"></a>根路径  
  
- For a type selected from the **Object Type** table, the **Paths to Root** table shows the unique type hierarchies that lead to root objects for all objects of the type, along with the number of references to the type that is above it in the hierarchy.  
  
- For an object selected from the instance of a type, **Paths to Root** shows a graph of the actual objects that hold a reference to the instance. 你可以悬停在对象的名称上以便在数据提示中查看其数据值。  
  
#### <a name="referenced-types--referenced-objects"></a>引用类型/引用对象  
  
- For a type selected from the **Object Type** table, the **Referenced Types** tab shows the size and number of referenced types held by all objects of the selected type.  
  
- For a selected instance of a type, **Referenced Objects** shows the objects that are held by the selected instance. 你可以悬停在该名称上以便在数据提示中查看其数据值。  
  
  **Circular references**  
  
  对象可以引用直接或间接保留对第一个对象引用的第二个对象。 When the memory analyzer encounters this situation, it stops expanding the reference path and adds a **[Cycle Detected]** annotation to the listing of the first object and stops.  
  
  **Root types**  
  
  内存分析程序将批注添加到描述要保留的引用类型的根对象：  
  
|批注|描述|  
|----------------|-----------------|  
|**Static variable** `VariableName`|静态变量。 `VariableName` 是变量的名称。|  
|**Finalization Handle**|来自终结器队列的引用|  
|**Local Variable**|局部变量。|  
|**Strong Handle**|来自对象句柄表的强引用的句柄。|  
|**Async. Pinned Handle**|来自对象句柄表的异步固定对象。|  
|**Dependent Handle**|来自对象句柄表的依赖对象。|  
|**Pinned Handle**|来自对象句柄表的固定强引用。|  
|**RefCount Handle**|来自对象句柄表的引用计数的对象。|  
|**SizedRef Handle**|在垃圾回收时间保留所有对象和对象根的集体闭合的近似大小的强句柄。|  
|**Pinned local variable**|固定局部变量。|  
  
### <a name="BKMK_Compare_two_memory_snapshots"></a> Compare two memory snapshots  
 你可以比较进程的两个转储文件以查找可能导致内存泄漏的原因。 第一个（早期）和第二个（晚期）文件的收集之间的间隔应足够大，（才能使）泄漏对象数目的增长显而易见。 若要比较两个文件：  
  
1. Open the second dump file, and then choose **Debug Managed Memory** on the **Minidump File Summary** page.  
  
2. On the memory analysis report page, open the **Select baseline** list, and then choose **Browse** to specify the first dump file.  
  
   The analyzer adds columns to the top pane of the report that display the difference between the **Count**, **Size**, and **Inclusive Size** of the types to those values in the earlier snapshot.  
  
   ![Diff columns in the type list](../misc/media/mngdmem-diffcolumns.png "MNGDMEM_DiffColumns")  
  
   A **Reference Count Diff** column is also added to the **Paths to Root** table.  
  
   ![Back to top](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [Contents](#BKMK_Contents)  
  
## <a name="see-also"></a>请参阅  
 [VS ALM TFS Blog: Using Visual Studio 2013 to Diagnose .NET Memory Issues in Production](https://devblogs.microsoft.com/devops/using-visual-studio-2013-to-diagnose-net-memory-issues-in-production/)   
 [Channel 9 &#124; Visual Studio TV &#124; Managed Memory Analysis](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Managed-Memory-Analysis)   
 [Channel 9 &#124; Visual Studio Toolbox &#124; Managed Memory Analysis in Visual Studio 2013](https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Managed-Memory-Analysis-in-Visual-Studio-2013)