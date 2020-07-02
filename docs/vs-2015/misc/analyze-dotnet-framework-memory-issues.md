---
title: 分析 .NET Framework 内存问题 |Microsoft Docs
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
ms.openlocfilehash: e89b3f04a3e0e1dcd0cc29e57e09b1c71fbc2279
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545543"
---
# <a name="analyze-net-framework-memory-issues"></a>分析 .NET Framework 内存问题
通过使用 Visual Studio 托管内存分析程序，在 .NET Framework 代码中查找内存泄漏和低效内存使用。 目标代码的最低 .NET Framework 版本为 .NET Framework 4.5。  
  
 内存分析工具*使用堆数据分析转储文件*中的信息，这些数据是应用程序内存中的对象的副本。 从 Visual Studio IDE 或通过使用其他系统工具，你可以收集转储 (.dmp) 文件。  
  
- 你可以分析单个快照以了解有关内存使用的对象类型的相对影响，并在你的应用中查找低效使用内存的代码。  
  
- 你还可以比较（*比较*）应用的两个快照，以便在代码中查找导致内存使用随时间增加的区域。  
  
  有关托管内存分析器的演练，请参阅在 Visual Studio ALM + Team Foundation Server 博客上[使用 Visual Studio 2013 诊断生产中的 .Net 内存问题](https://devblogs.microsoft.com/devops/using-visual-studio-2013-to-diagnose-net-memory-issues-in-production/)。  
  
## <a name="contents"></a><a name="BKMK_Contents"></a> 内容  
 [.NET Framework 应用中的内存使用](#BKMK_Memory_use_in__NET_Framework_apps)  
  
 [在应用中标识内存问题](#BKMK_Identify_a_memory_issue_in_an_app)  
  
 [收集内存快照](#BKMK_Collect_memory_snapshots)  
  
 [分析内存使用](#BKMK_Analyze_memory_use)  
  
## <a name="memory-use-in-net-framework-apps"></a><a name="BKMK_Memory_use_in__NET_Framework_apps"></a>.NET Framework 应用中的内存使用  
 .NET Framework 为垃圾回收运行时，这样在大多数应用中，内存使用不会成为问题。 但在长时间运行的应用程序中（如 Web 服务和应用程序），以及在只有有限内存的设备中，对象在内存中的累积会影响应用以及运行应用的设备的性能。 如果垃圾回收器运行过于频繁，或者如果强制操作系统在 RAM 和磁盘之间移动内存，则过多占用内存会停止应用程序和资源所在的计算机。 在最坏情况下，应用会因“内存不足”异常而崩溃。  
  
 .NET*托管堆*是虚拟内存区域，其中存储了应用创建的引用对象。 对象的生存期由垃圾收集器 (GC) 管理。 垃圾收集器使用引用以跟踪占用内存块的对象。 当创建对象并将其分配到变量时，就会创建一个引用。 单个对象可以具有多个引用。 例如，对一个对象的其他引用可以通过将该对象添加到类、集合或其他数据结构来创建，也可以通过将该对象分配给第二个变量来创建。 创建引用的一个不太明显的方式是通过一个对象将处理程序添加到另一个对象的事件。 在这种情况下，第二个对象保留对第一个对象的引用，直到该处理程序被显式删除或第二个对象被销毁。  
  
 对于每个应用程序，GC 维护跟踪由应用程序所引用的对象的引用树。 *引用树*具有一组根，其中包括全局对象和静态对象，以及关联的线程堆栈和动态实例化的对象。 如果一个对象具有至少一个保存对其引用的父对象，则该对象为根对象。 只有当应用程序中的其他对象或变量都不具有对它的引用时，GC 才能回收对象的内存。  
  
 ![返回页首](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [内容](#BKMK_Contents)  
  
## <a name="identify-a-memory-issue-in-an-app"></a><a name="BKMK_Identify_a_memory_issue_in_an_app"></a>确定应用中的内存问题  
 内存问题的最明显症状是应用的性能，尤其是如果随着时间的推移性能降低。 当你的应用运行时，其他应用的性能下降，也可能表示存在内存问题。 如果怀疑出现内存问题，请使用任务管理器或[Windows 性能监视器](https://technet.microsoft.com/library/cc749249.aspx)之类的工具进行进一步调查。 例如，查看无法解释为内存泄漏可能来源的内存总大小的增长：  
  
 ![资源监视器中一致的内存增长](../misc/media/mngdmem-resourcemanagerconsistentgrowth.png "MNGDMEM_ResourceManagerConsistentGrowth")  
  
 你可能还会注意到内存峰值，它们比就你所知的代码建议的值大，可能指向某个过程内的低效内存使用：  
  
 ![资源监视器中的内存峰值](../misc/media/mngdmem-resourcemanagerspikes.png "MNGDMEM_ResourceManagerSpikes")  
  
## <a name="collect-memory-snapshots"></a><a name="BKMK_Collect_memory_snapshots"></a>收集内存快照  
 内存分析工具分析包含堆信息的*转储文件*中的信息。 你可以在 Visual Studio 中创建转储文件，也可以使用[ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx)从[Windows Sysinternals](https://technet.microsoft.com/sysinternals)的工具。 请参阅 Visual Studio 调试器团队博客上[的什么是转储，以及如何创建一个](https://blogs.msdn.microsoft.com/debugger/2009/12/30/what-is-a-dump-and-how-do-i-create-one/)。  
  
> [!NOTE]
> 大部分工具可以收集附带或不附带完整堆内存数据的转储信息。 Visual Studio 内存分析程序需要完整的堆信息。  
  
 **从 Visual Studio 收集转储**  
  
1. 你可以针对从 Visual Studio 项目开始的进程创建一个转储文件，或者也可以将调试器附加到正在运行的进程。 请参阅[附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)。  
  
2. 停止执行。 当你在 "**调试**" 菜单上选择 "**全部中断**" 时，或者在异常或断点处停止调试器  
  
3. 在 "**调试**" 菜单上，选择 "**将转储另存为**"。 在 "将**转储另存为**" 对话框中，指定位置，并确保在 "**保存类型**" 列表中选择了 "**带堆的小型转储**（默认值）"。  
  
   **比较两个内存快照**  
  
   若要分析应用内存使用中的增长，请从该应用的单个实例收集两个转储文件。  
  
   ![返回页首](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [内容](#BKMK_Contents)  
  
## <a name="analyze-memory-use"></a><a name="BKMK_Analyze_memory_use"></a>分析内存使用情况  
 [筛选对象的列表](#BKMK_Filter_the_list_of_objects) **&#124;** [从单个快照分析中的内存数据](#BKMK_Analyze_memory_data_in_from_a_single_snapshot) **&#124;** [比较两个内存快照](#BKMK_Compare_two_memory_snapshots)  
  
 若要针对内存使用问题分析转储文件：  
  
1. 在 Visual Studio 中，选择 "**文件**"，**打开**并指定转储文件。  
  
2. 在 "**小型转储文件摘要**" 页上，选择 "**调试托管内存**"。  
  
    ![转储文件摘要页](../misc/media/mngdmem-dumpfilesummary.png "MNGDMEM_DumpFileSummary")  
  
   内存分析程序启动调试会话以分析文件并且在“堆视图”页面上显示结果：  
  
   ![返回页首](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [内容](#BKMK_Contents)  
  
### <a name="filter-the-list-of-objects"></a><a name="BKMK_Filter_the_list_of_objects"></a>筛选对象列表  
 默认情况下，内存分析程序在内存快照中筛选对象列表，以便只显示用户代码的类型和实例，并且只显示那些总包含大小超过总堆大小阈值百分比的类型。 可以在 "**视图设置**" 列表中更改这些选项：  
  
|“属性”|描述|  
|-|-|  
|**启用“仅我的代码”**|“仅我的代码”将隐藏最常用的系统对象，以便只有你创建的类型显示在列表中。<br /><br /> 你还可以在 Visual Studio 的 "**选项**" 对话框中设置 "仅我的代码" 选项。 在 **“调试”** 菜单上，选择 **“选项和设置”** 。 在 "**调试** / **常规**" 选项卡中，选择或清除**仅我的代码**。|  
|**折叠小对象**|**折叠小对象**将隐藏总包含大小小于总堆大小0.5% 的所有类型。|  
  
 还可以通过在**搜索**框中输入字符串来筛选类型列表。 该列表只显示那些名称中包含字符串的类型。  
  
 ![返回页首](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [内容](#BKMK_Contents)  
  
### <a name="analyze-memory-data-in-from-a-single-snapshot"></a><a name="BKMK_Analyze_memory_data_in_from_a_single_snapshot"></a>从单个快照分析中的内存数据  
 Visual Studio 启动新的调试会话以分析文件，并且在“堆视图”窗口中显示内存数据。  
  
 ![“对象类型”列表](../misc/media/dbg-mma-objecttypelist.png "DBG_MMA_ObjectTypeList")  
  
 ![返回页首](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [内容](#BKMK_Contents)  
  
#### <a name="object-type-table"></a>对象类型表  
 上表列出了在内存中保留的对象的类型。  
  
- **Count**显示快照中类型实例的数量。  
  
- **Size （字节）** 是该类型的所有实例的大小，不包括其引用的对象的大小。 必须向  
  
- **非独占大小（字节）** 包含被引用对象的大小。  
  
  您可以在 "**对象类型**" 列中选择实例图标（![对象类型列中的实例图标](../misc/media/dbg-mma-instancesicon.png "DBG_MMA_InstancesIcon")），以查看类型实例的列表。  
  
#### <a name="instance-table"></a>实例表  
 ![实例表](../misc/media/dbg-mma-instancestable.png "DBG_MMA_InstancesTable")  
  
- **实例**是对象的内存位置，用作对象的对象标识符  
  
- **值**显示值类型的实际值。 你可以悬停在引用类型的名称上以便在数据提示中查看其数据值。  
  
   ![数据提示中的实例值](../misc/media/dbg-mma-instancevaluesindatatip.png "DBG_MMA_InstanceValuesInDataTip")  
  
- **Size （字节）** 是对象的大小，不包括其引用的对象的大小。 必须向  
  
- **非独占大小（字节）** 包含被引用对象的大小。  
  
  默认情况下，按**非独占大小（字节）** 对类型和实例进行排序。 在列表中选择一个列标题以更改排序顺序。  
  
#### <a name="paths-to-root"></a>根路径  
  
- 对于从 "**对象类型**" 表中选择的类型，"**根路径的路径**" 将显示为该类型的所有对象的根对象提供的唯一类型层次结构，以及层次结构中对该类型之上的类型的引用数目。  
  
- 对于从类型实例中选择的对象，**根路径**显示包含对实例的引用的实际对象的关系图。 你可以悬停在对象的名称上以便在数据提示中查看其数据值。  
  
#### <a name="referenced-types--referenced-objects"></a>引用类型/引用对象  
  
- 对于从 "**对象类型**" 表中选择的类型，"**引用的类型**" 选项卡显示所选类型的所有对象所包含的被引用类型的大小和数目。  
  
- 对于类型的选定实例，**被引用对象**将显示所选实例持有的对象。 你可以悬停在该名称上以便在数据提示中查看其数据值。  
  
  **循环引用**  
  
  对象可以引用直接或间接保留对第一个对象引用的第二个对象。 当内存分析器遇到这种情况时，它将停止展开引用路径，并将 "**检测到循环**数" 批注添加到第一个对象的列表中，然后停止。  
  
  **根类型**  
  
  内存分析程序将批注添加到描述要保留的引用类型的根对象：  
  
|Annotation|描述|  
|----------------|-----------------|  
|**“静态变量”** `VariableName`|静态变量。 `VariableName` 是变量的名称。|  
|**终结句柄**|来自终结器队列的引用|  
|**局部变量**|局部变量。|  
|**强句柄**|来自对象句柄表的强引用的句柄。|  
|**异步.固定句柄**|来自对象句柄表的异步固定对象。|  
|**依赖句柄**|来自对象句柄表的依赖对象。|  
|**固定句柄**|来自对象句柄表的固定强引用。|  
|**RefCount 句柄**|来自对象句柄表的引用计数的对象。|  
|**SizedRef 句柄**|在垃圾回收时间保留所有对象和对象根的集体闭合的近似大小的强句柄。|  
|**固定局部变量**|固定局部变量。|  
  
### <a name="compare-two-memory-snapshots"></a><a name="BKMK_Compare_two_memory_snapshots"></a>比较两个内存快照  
 你可以比较进程的两个转储文件以查找可能导致内存泄漏的原因。 第一个（早期）和第二个（晚期）文件的收集之间的间隔应足够大，（才能使）泄漏对象数目的增长显而易见。 若要比较两个文件：  
  
1. 打开第二个转储文件，然后在 "**小型转储文件摘要**" 页上选择 "**调试托管内存**"。  
  
2. 在 "内存分析报表" 页上，打开 "**选择基线**" 列表，然后选择 "**浏览**" 以指定第一个转储文件。  
  
   分析器将列添加到报表的顶部窗格中，该窗格显示类型到以前的快照中的值的**计数**、**大小**和**非独占大小**之间的差异。  
  
   ![类型列表中的差异列](../misc/media/mngdmem-diffcolumns.png "MNGDMEM_DiffColumns")  
  
   **引用计数差异**列还将添加到根表的**路径**中。  
  
   ![返回页首](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [内容](#BKMK_Contents)  
  
## <a name="see-also"></a>另请参阅  
 [VS ALM TFS 博客：使用 Visual Studio 2013 诊断生产中的 .NET 内存问题](https://devblogs.microsoft.com/devops/using-visual-studio-2013-to-diagnose-net-memory-issues-in-production/)   
 [第9频道 &#124; Visual Studio TV &#124; 托管内存分析](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Managed-Memory-Analysis)   
 [第9频道 &#124; Visual Studio 工具箱 &#124; 托管内存分析在 Visual Studio 2013](https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Managed-Memory-Analysis-in-Visual-Studio-2013)