---
title: 内存使用情况 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: bbb58d6c-3362-4ca3-8e87-64b2d4415bf6
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 132e6252662ed765630764dabca26b22f868a315
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704878"
---
# <a name="memory-usage"></a>内存使用率
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用调试器集成的 **内存使用率** 诊断工具在进行调试时查找内存泄漏和低效内存。 通过内存使用率工具可以拍摄托管和本机内存堆的一个或多个快照  。 可以收集 .NET、本机或混合模式（.NET 和本机）应用的快照。  
  
- 你可以分析单个快照以了解有关内存使用的对象类型的相对影响，并在你的应用中查找低效使用内存的代码。  
  
- 你还可以比较 (diff) 一个应用的两个快照，以便在你的代码中查找导致内存使用随时间增加的区域。  
  
  下图显示 Visual Studio 2015 Update 1 中的“诊断工具”  窗口：  
  
  ![DiagnosticTools&#45;Update1](../profiling/media/diagnostictools-update1.png "DiagnosticTools-Update1")  
  
  虽然可以随时在 **内存使用率** 工具中收集内存快照，不过可以使用 Visual Studio 调试器在调查性能问题时控制应用程序的执行方式。 断点设置、步进、全部中断和其他调试器操作可以帮助将性能调查集中在最相关的代码路径上。 在应用运行期间执行这些操作可以从代码中消除不感兴趣的噪声，并可以显著减少用于诊断问题所花费的时间量。  
  
  还可以在调试器外部使用内存工具。 请参阅 [Memory Usage without Debugging](https://msdn.microsoft.com/library/8883bc5f-df86-4f84-aa2b-a21150f499b0)。  
  
> [!NOTE]
> **自定义分配器支持** 本机内存探查器的工作原理是在运行时收集 [ETW](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx) 分配事件数据。  CRT 和 Windows SDK 中的分配器在源级别上注释，因此可以捕获其分配数据。  如果你正在编写你自己的分配器，则返回一个指向新分配的堆内存的任何函数可用 [__declspec](https://msdn.microsoft.com/library/832db681-e8e1-41ca-b78c-cd9d265cdb87)（分配器）进行修饰，如此 myMalloc 示例所示：  
>   
> `__declspec(allocator) void* myMalloc(size_t size)`  
  
## <a name="analyze-memory-use-with-the-debugger"></a>使用调试器分析内存使用  
  
> [!NOTE]
> 因为收集内存数据可能会影响本机或混合模式应用的调试性能，所以内存快照在默认情况下处于禁用状态。 若要启用快照本机或混合模式应用程序，请启动调试会话 (快捷键：F5）。 当 **“诊断工具”** 窗口出现时，选择“内存使用率”选项卡，然后选择 **“启用快照”**。  
>   
> ![启用快照](../profiling/media/dbgdiag-mem-mixedtoolbar-enablesnapshot.png "DBGDIAG_MEM_MixedToolbar_EnableSnapshot")  
>   
> 停止（快捷键：**Shift + F5**) 并重新启动调试。  
  
 每当要捕获内存状态时，请在 **“内存使用率”** 摘要工具栏上选择 **“拍摄快照”** 。  
  
 ![拍摄快照](../profiling/media/dbgdiag-mem-mixedtoolbar-takesnapshot.png "DBGDIAG_MEM_MixedToolbar_TakeSnapshot")  
  
> [!TIP]
> - 若要为进行内存比较而创建基线，请考虑在调试会话开始时拍摄快照。  
>   - 因为在应用经常分配并取消分配内存时捕获感兴趣的操作的内存配置文件十分具有挑战性，所以请在操作开始和结束时设置断点，或逐步执行操作以查找内存变化的确切点。  
  
## <a name="viewing-memory-snapshot-details"></a>查看内存快照详细信息  
 内存使用率摘要表中的行会列出在调试会话期间拍摄的快照。  
  
 行的列取决于在项目属性中选择的调试模式：.NET、本机或混合（.NET 和本机）。  
  
- **“托管对象”** 和 **“本机分配”** 列显示拍摄快照时 .NET 和本机内存中的对象数。  
  
- **“托管堆大小”** 和 **“本机堆大小”** 列显示 .NET 和本机堆中的字节数  
  
- 拍摄多个快照时，摘要表的单元格包含行快照与前一个快照之间的值变化。  
  
   ![内存摘要表单元格](../profiling/media/dbgdiag-mem-summarytablecell.png "DBGDIAG_MEM_SummaryTableCell")  
  
  **查看详细信息报表：**  
  
- 若要仅查看所选快照的详细信息，请选择当前链接。  
  
- 若要查看当前快照与前一个快照之间的差异的详细信息，请选择更改链接。  
  
  报告会出现在单独的窗口中。  
  
## <a name="memory-usage-details-reports"></a>内存使用率详细信息报告  
  
### <a name="managed-types-reports"></a>托管类型报告  
 在内存使用率摘要表中选择 **“托管对象”** 或 **“托管堆大小”** 单元格的当前链接。  
  
 ![调试器托管的类型报表 - 根路径](../profiling/media/dbgdiag-mem-managedtypesreport-pathstoroot.png "DBGDIAG_MEM_ManagedTypesReport_PathsToRoot")  
  
 顶部窗格会显示快照中类型的计数和大小，包括由类型引用的所有对象的大小（**“非独占大小”**）。  
  
 底部窗格中的 **“根的路径”** 树显示引用上部窗格中选择的类型的对象。 仅当引用某个对象的最后一个类型已释放时，.NET Framework 垃圾回收器才清理该对象的内存。  
  
 **“引用的类型”** 树显示上部窗格中选择的类型所持有的引用。  
  
 ![托管的引用类型报表视图](../profiling/media/dbgdiag-mem-managedtypesreport-referencedtypes.png "DBGDIAG_MEM_ManagedTypesReport_ReferencedTypes")  
  
 若要显示上部窗格中所选类型的实例，请选择 ![实例图标](../profiling/media/dbgdiag-mem-instanceicon.png "DBGDIAG_MEM_InstanceIcon") 图标。  
  
 ![实例视图](../profiling/media/dbgdiag-mem-managedtypesreport-instances.png "DBGDIAG_MEM_ManagedTypesReport_Instances")  
  
 **“实例”** 视图显示上部窗格的快照中所选对象的实例。 “根的路径”和“引用的对象”窗格显示引用所选实例的对象以及所选实例引用的类型。 当调试器在拍摄快照的点停止时，可以将鼠标悬停在“值”单元格上方以在工具提示中显示对象的值。  
  
### <a name="native-type-reports"></a>本机类型报告  
 在 **“诊断工具”** 窗口的内存使用率摘要表中选择 **“本机分配”** 或 **“本机堆大小”** 单元格的当前链接。  
  
 ![本机类型视图](../profiling/media/dbgdiag-mem-native-typesview.png "DBGDIAG_MEM_Native_TypesView")  
  
 **“类型视图”** 显示快照中类型的数量和大小。  
  
- 选择所选类型的实例图标（![“对象类型”列中的实例图标](../misc/media/dbg-mma-instancesicon.png "DBG_MMA_InstancesIcon")）可显示有关快照中所选类型的对象信息。  
  
     **“实例”** 视图显示所选类型的每个实例。 选择实例可显示导致在 **“分配调用堆栈”** 窗格中创建实例的调用堆栈。  
  
     ![实例视图](../profiling/media/dbgdiag-mem-native-instances.png "DBGDIAG_MEM_Native_Instances")  
  
- 在 **“视图模式”** 列表中选择 **“堆栈视图”** 可查看所选类型的分配堆栈。  
  
     ![堆栈视图](../profiling/media/dbgdiag-mem-native-stacksview.png "DBGDIAG_MEM_Native_StacksView")  
  
### <a name="change-diff-reports"></a>更改（差异）报告  
  
- 在 **“诊断工具”** 窗口上的 **“内存使用率”** 选项卡的摘要表单元格中选择更改链接。  
  
   ![选择更改（差异）报告](../profiling/media/dbgdiag-mem-choosediffreport.png "DBGDIAG_MEM_ChooseDiffReport")  
  
- 在托管或本机报告的 **“与之比较的对象”** 列表中选择快照。  
  
   ![从“比较对象”列表中选择一个快照](../profiling/media/dbgdiag-mem-choosecompareto.png "DBGDIAG_MEM_ChooseCompareTo")  
  
  更改报告会向基本报告添加一些列（使用 **“(差异)”** 进行标记），这些列显示基本快照值与比较快照之间的差异。 下面是本机类型视图差异报告的可能外观：  
  
  ![本机类型差异视图](../profiling/media/dbgdiag-mem-native-typesviewdiff.png "DBGDIAG_MEM_Native_TypesViewDiff")  
  
## <a name="blogs-and-videos"></a>博客和视频  
 [Visual Studio 2015 中的“诊断工具”调试器窗口](http://blogs.msdn.com/b/visualstudioalm/archive/2015/01/16/diagnostic-tools-debugger-window-in-visual-studio-2015.aspx)  
  
 [博客：在 Visual Studio 2015 中调试时的内存使用情况工具](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/13/memory-usage-tool-while-debugging-in-visual-studio-2015.aspx)  
  
 [Visual C++ 博客：VS2015 预览版中的本机内存诊断](http://blogs.msdn.com/b/vcblog/archive/2014/11/21/native-memory-diagnostics-in-vs2015-preview.aspx)  
  
 [Visual C++ 博客：Visual Studio 2015 CTP 的本机内存诊断工具](http://blogs.msdn.com/b/vcblog/archive/2014/06/04/native-memory-diagnostic-tools-for-visual-studio-14-ctp1.aspx)
