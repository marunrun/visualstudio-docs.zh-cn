---
title: 分析.NET Framework 内存问题 |Microsoft Docs
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
ms.openlocfilehash: 885f96a4e1e43fe422c6fd9cfaa414fe5871bce1
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65688577"
---
# <a name="analyze-net-framework-memory-issues"></a>分析 .NET Framework 内存问题
通过使用 Visual Studio 托管内存分析程序，在 .NET Framework 代码中查找内存泄漏和低效内存使用。 目标代码的最低 .NET Framework 版本为 .NET Framework 4.5。  
  
 内存分析工具分析中的信息*转储与堆数据的文件*的应用程序的内存中对象的副本。 从 Visual Studio IDE 或通过使用其他系统工具，你可以收集转储 (.dmp) 文件。  
  
- 你可以分析单个快照以了解有关内存使用的对象类型的相对影响，并在你的应用中查找低效使用内存的代码。  
  
- 此外可以比较 (*差异*) 两个快照应用程序以在代码中找到的区域，导致内存使用随时间增加。  
  
  托管的内存分析程序的演练，请参阅[到生产中诊断.NET 内存问题使用 Visual Studio 2013](http://blogs.msdn.com/b/visualstudioalm/archive/2013/06/20/using-visual-studio-2013-to-diagnose-net-memory-issues-in-production.aspx) Visual Studio ALM + Team Foundation Server 博客上。  
  
## <a name="BKMK_Contents"></a> 内容  
 [.NET Framework 应用程序中的内存使用](#BKMK_Memory_use_in__NET_Framework_apps)  
  
 [标识内存问题的应用程序中](#BKMK_Identify_a_memory_issue_in_an_app)  
  
 [收集内存快照](#BKMK_Collect_memory_snapshots)  
  
 [分析内存使用](#BKMK_Analyze_memory_use)  
  
## <a name="BKMK_Memory_use_in__NET_Framework_apps"></a> .NET Framework 应用程序中的内存使用  
 .NET Framework 为垃圾回收运行时，这样在大多数应用中，内存使用不会成为问题。 但在长时间运行的应用程序中（如 Web 服务和应用程序），以及在只有有限内存的设备中，对象在内存中的累积会影响应用以及运行应用的设备的性能。 如果垃圾回收器运行过于频繁，或者如果强制操作系统在 RAM 和磁盘之间移动内存，则过多占用内存会停止应用程序和资源所在的计算机。 在最坏情况下，应用会因“内存不足”异常而崩溃。  
  
 .NET*托管的堆*是所创建的应用程序的引用对象的存储位置的虚拟内存区域。 对象的生存期由垃圾收集器 (GC) 管理。 垃圾收集器使用引用以跟踪占用内存块的对象。 当创建对象并将其分配到变量时，就会创建一个引用。 单个对象可以具有多个引用。 例如，对一个对象的其他引用可以通过将该对象添加到类、集合或其他数据结构来创建，也可以通过将该对象分配给第二个变量来创建。 创建引用的一个不太明显的方式是通过一个对象将处理程序添加到另一个对象的事件。 在这种情况下，第二个对象保留对第一个对象的引用，直到该处理程序被显式删除或第二个对象被销毁。  
  
 对于每个应用程序，GC 维护跟踪由应用程序所引用的对象的引用树。 *引用树*具有一组根，其中包括全局和静态对象，以及相关联的线程堆栈和动态实例化的对象。 如果一个对象具有至少一个保存对其引用的父对象，则该对象为根对象。 只有当应用程序中的其他对象或变量都不具有对它的引用时，GC 才能回收对象的内存。  
  
 ![返回页首](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目录](#BKMK_Contents)  
  
## <a name="BKMK_Identify_a_memory_issue_in_an_app"></a> 标识内存问题的应用程序中  
 内存问题的最明显症状是应用的性能，尤其是如果随着时间的推移性能降低。 当你的应用运行时，其他应用的性能下降，也可能表示存在内存问题。 如果你怀疑存在内存问题，使用任务管理器等的工具或[Windows 性能监视器](https://technet.microsoft.com/library/cc749249.aspx)若要进一步调查。 例如，查看无法解释为内存泄漏可能来源的内存总大小的增长：  
  
 ![资源监视器中一致的内存增长](../misc/media/mngdmem-resourcemanagerconsistentgrowth.png "MNGDMEM_ResourceManagerConsistentGrowth")  
  
 你可能还会注意到内存峰值，它们比就你所知的代码建议的值大，可能指向某个过程内的低效内存使用：  
  
 ![在资源管理器的内存峰值](../misc/media/mngdmem-resourcemanagerspikes.png "MNGDMEM_ResourceManagerSpikes")  
  
## <a name="BKMK_Collect_memory_snapshots"></a> 收集内存快照  
 内存分析工具分析中的信息*转储文件*包含堆信息。 你可以在 Visual Studio 中，创建转储文件，或者可以使用之类的工具[ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx)从[Windows Sysinternals](https://technet.microsoft.com/sysinternals)。 请参阅[什么是转储，以及如何创建？](http://blogs.msdn.com/b/debugger/archive/2009/12/30/what-is-a-dump-and-how-do-i-create-one.aspx) Visual Studio 调试器团队博客上。  
  
> [!NOTE]
> 大部分工具可以收集附带或不附带完整堆内存数据的转储信息。 Visual Studio 内存分析程序需要完整的堆信息。  
  
 **若要从 Visual Studio 收集转储**  
  
1. 你可以针对从 Visual Studio 项目开始的进程创建一个转储文件，或者也可以将调试器附加到正在运行的进程。 请参阅[将附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)。  
  
2. 停止执行。 在调试器停止时选择**全部中断**上**调试**菜单中，或在发生异常或断点处  
  
3. 上**调试**菜单中，选择**转储另存为**。 中**转储另存为**对话框框中，指定的位置并确保选中**小型转储与堆**（默认值） 中选择**另存为类型**列表。  
  
   **要比较两个内存快照**  
  
   若要分析应用内存使用中的增长，请从该应用的单个实例收集两个转储文件。  
  
   ![返回页首](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目录](#BKMK_Contents)  
  
## <a name="BKMK_Analyze_memory_use"></a> 分析内存使用  
 [筛选对象列表](#BKMK_Filter_the_list_of_objects) **&#124;** [分析中从单个快照的内存数据](#BKMK_Analyze_memory_data_in_from_a_single_snapshot) **&#124;** [比较两个内存快照](#BKMK_Compare_two_memory_snapshots)  
  
 若要针对内存使用问题分析转储文件：  
  
1. 在 Visual Studio 中，选择**文件**，**打开**并指定转储文件。  
  
2. 上**小型转储文件摘要**页上，选择**调试托管内存**。  
  
    ![转储文件摘要页](../misc/media/mngdmem-dumpfilesummary.png "MNGDMEM_DumpFileSummary")  
  
   内存分析程序启动调试会话以分析文件并且在“堆视图”页面上显示结果：  
  
   ![返回页首](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目录](#BKMK_Contents)  
  
### <a name="BKMK_Filter_the_list_of_objects"></a> 筛选对象列表  
 默认情况下，内存分析程序在内存快照中筛选对象列表，以便只显示用户代码的类型和实例，并且只显示那些总包含大小超过总堆大小阈值百分比的类型。 您可以更改这些选项在**视图设置**列表：  
  
|||  
|-|-|  
|**启用“仅我的代码”**|“仅我的代码”将隐藏最常用的系统对象，以便只有你创建的类型显示在列表中。<br /><br /> 此外可以在 Visual Studio 中设置仅我的代码选项**选项**对话框。 在 **“调试”** 菜单上，选择 **“选项和设置”**。 在中**调试**/**常规**选项卡上，选择或清除**仅我的代码**。|  
|**隐藏小型对象**|**隐藏小型对象**隐藏总包含大小是小于总堆大小的 0.5%的所有类型。|  
  
 此外可以通过输入中的字符串来筛选类型列表**搜索**框。 该列表只显示那些名称中包含字符串的类型。  
  
 ![返回页首](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目录](#BKMK_Contents)  
  
### <a name="BKMK_Analyze_memory_data_in_from_a_single_snapshot"></a> 分析中从单个快照的内存数据  
 Visual Studio 启动新的调试会话以分析文件，并且在“堆视图”窗口中显示内存数据。  
  
 ![对象类型列表](../misc/media/dbg-mma-objecttypelist.png "DBG_MMA_ObjectTypeList")  
  
 ![返回页首](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目录](#BKMK_Contents)  
  
#### <a name="object-type-table"></a>对象类型表  
 上表列出了在内存中保留的对象的类型。  
  
- **计数**快照中显示该类型的实例数。  
  
- **大小 （字节）** 是不包括其保留对引用对象的大小的类型的所有实例的大小。 必须向  
  
- **非独占大小 （字节）** 包括被引用对象的大小。  
  
  您可以选择实例图标 (![对象类型列中的实例图标](../misc/media/dbg-mma-instancesicon.png "DBG_MMA_InstancesIcon")) 中**对象类型**列可查看的实例的列表类型。  
  
#### <a name="instance-table"></a>实例表  
 ![实例表](../misc/media/dbg-mma-instancestable.png "DBG_MMA_InstancesTable")  
  
- **实例**是可作为对象的对象标识符的对象的内存位置  
  
- **值**显示值类型的实际值。 你可以悬停在引用类型的名称上以便在数据提示中查看其数据值。  
  
   ![实例数据提示中的值](../misc/media/dbg-mma-instancevaluesindatatip.png "DBG_MMA_InstanceValuesInDataTip")  
  
- **大小 （字节）** 是对象，其中不包括其保留对引用对象的大小的大小。 必须向  
  
- **非独占大小 （字节）** 包括被引用对象的大小。  
  
  默认情况下，类型和实例按排序**非独占大小 （字节）**。 在列表中选择一个列标题以更改排序顺序。  
  
#### <a name="paths-to-root"></a>根路径  
  
- 从所选类型**对象类型**表中，**根路径**表显示的唯一类型层次结构的类型，以及对引用数的所有对象的根对象到可付诸实践在层次结构中其上方的类型。  
  
- 从一个类型的实例选择的对象**根路径**显示实际包含的对象实例的引用关系图。 你可以悬停在对象的名称上以便在数据提示中查看其数据值。  
  
#### <a name="referenced-types--referenced-objects"></a>引用类型/引用对象  
  
- 从所选类型**对象类型**表中，**引用的类型**选项卡显示的大小和数量的所选类型的所有对象所都持有的引用的类型。  
  
- 所选实例的类型，**引用的对象**显示所选实例所持有的对象。 你可以悬停在该名称上以便在数据提示中查看其数据值。  
  
  **循环引用**  
  
  对象可以引用直接或间接保留对第一个对象引用的第二个对象。 当内存分析器遇到这种情况下时，它将停止展开引用路径，并添加 **[检测到循环]** 批注相对于列表的第一个对象并停止。  
  
  **根类型**  
  
  内存分析程序将批注添加到描述要保留的引用类型的根对象：  
  
|批注|描述|  
|----------------|-----------------|  
|**静态变量** `VariableName`|静态变量。 `VariableName` 是变量的名称。|  
|**终结句柄**|来自终结器队列的引用|  
|**本地变量**|局部变量。|  
|**强句柄**|来自对象句柄表的强引用的句柄。|  
|**异步。固定句柄**|来自对象句柄表的异步固定对象。|  
|**依赖句柄**|来自对象句柄表的依赖对象。|  
|**固定句柄**|来自对象句柄表的固定强引用。|  
|**RefCount 句柄**|来自对象句柄表的引用计数的对象。|  
|**SizedRef 句柄**|在垃圾回收时间保留所有对象和对象根的集体闭合的近似大小的强句柄。|  
|**固定局部变量**|固定局部变量。|  
  
### <a name="BKMK_Compare_two_memory_snapshots"></a> 比较两个内存快照  
 你可以比较进程的两个转储文件以查找可能导致内存泄漏的原因。 第一个（早期）和第二个（晚期）文件的收集之间的间隔应足够大，（才能使）泄漏对象数目的增长显而易见。 若要比较两个文件：  
  
1. 打开第二个转储文件，并选择**调试托管内存**上**小型转储文件摘要**页。  
  
2. 在内存分析报表页上，打开**选择基线**列表，，然后选择**浏览**来指定第一个转储文件。  
  
   分析器将列添加到显示之间的差的报表的顶部窗格**计数**，**大小**，并**非独占大小**到中的那些值的类型以前的快照。  
  
   ![类型列表中的差异列](../misc/media/mngdmem-diffcolumns.png "MNGDMEM_DiffColumns")  
  
   一个**引用计数差异**还将列添加到**根路径**表。  
  
   ![返回页首](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [目录](#BKMK_Contents)  
  
## <a name="see-also"></a>请参阅  
 [VS ALM TFS 博客：使用 Visual Studio 2013 诊断生产中的.NET 内存问题](http://blogs.msdn.com/b/visualstudioalm/archive/2013/06/20/using-visual-studio-2013-to-diagnose-net-memory-issues-in-production.aspx)   
 [第 9 频道&#124;Visual Studio 电视&#124;托管内存分析](http://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Managed-Memory-Analysis)   
 [第 9 频道&#124;Visual Studio 工具箱&#124;托管在 Visual Studio 2013 中的内存分析](http://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Managed-Memory-Analysis-in-Visual-Studio-2013)