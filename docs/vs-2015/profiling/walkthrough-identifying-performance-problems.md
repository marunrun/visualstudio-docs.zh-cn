---
title: 演练：确定性能问题 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, walkthroughs
- performance tools, walkthroughs
- performance, analyzing
- profiling applications, walkthroughs
ms.assetid: 36f6f123-0c14-4763-99c3-bd60ecb95b87
caps.latest.revision: 58
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6bc4135b9b861a460295c67c576405edd5c63211
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65695005"
---
# <a name="walkthrough-identifying-performance-problems"></a>演练：确定性能问题
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练演示如何分析应用程序以确定性能问题。  
  
 在本演练中，你将逐步完成分析托管应用程序并使用采样和检测来隔离并确定应用程序中的性能问题的过程。  
  
 在本演练中，你将遵循以下步骤：  
  
- 使用采样方法分析应用程序。  
  
- 分析被采样的分析结果，以查找并修复性能问题。  
  
- 使用检测方法分析应用程序。  
  
- 分析被检测的分析结果，以查找并修复性能问题。  
  
## <a name="prerequisites"></a>先决条件  
  
- 对 C# 有中等程度的理解。  
  
- [PeopleTrax 示例](../profiling/peopletrax-sample-profiling-tools.md)的副本。  
  
  若要使用分析提供的信息，最好有可用的调试符号信息。  
  
## <a name="profiling-by-using-the-sampling-method"></a>使用采样方法进行分析  
 采样是一种分析方法，通过此方法可定期对相关进程进行轮询以确定活动的函数。 生成的数据提供对进程进行采样时相关函数位于调用堆栈顶部的频率计数。  
  
#### <a name="to-profile-an-application-by-using-the-sampling-method"></a>使用采样方法分析应用程序  
  
1. 使用管理员权限打开 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]。 需要以管理员身份运行才能进行分析。  
  
2. 打开 PeopleTrax 解决方案。  
  
     PeopleTrax 解决方案现在将填充解决方案资源管理器。  
  
3. 将项目配置设置设置为“发布”****。  
  
     应使用发布版本检测应用程序中的性能问题。 建议使用发布版本进行分析，因为调试版本中编译有其他的信息，这可能会对性能产生负面影响，并且不能准确地阐明性能问题。  
  
4. 在“分析”  菜单上，单击“启动性能向导” 。  
  
     将出现“性能向导”。  
  
5. 请确保已选择了“CPU 采样(建议)”****，然后单击“下一步”****。  
  
6. 在“要以哪个应用程序为目标进行分析?”**** 中，选择“PeopleTrax”，然后单击“下一步”****。  
  
     [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 将生成项目并开始分析应用程序。 此时将显示 " **PeopleTrax** " 应用程序窗口。  
  
7. 单击“获取人员”****。  
  
8. 单击“导出数据”****。  
  
     记事本随即打开并显示其中包含从“PeopleTrax”**** 导出的数据的新文件。  
  
9. 关闭记事本，然后关闭“PeopleTrax”**** 应用程序。  
  
     探查器将生成分析数据 (\*.vsp) 文件，列出“性能资源管理器”窗口的“报表”分区中的文件名，并在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 的主窗口中自动加载数据文件的“摘要”**** 视图。  
  
#### <a name="to-analyze-sampled-profiling-results"></a>分析被采样的分析结果  
  
1. “摘要”视图显示以下内容：分析运行过程中 CPU 使用率的时间线、“热路径”**** 列表（此列表表示应用程序最活跃的调用树的分支）和“执行单个工作最多的函数”的**** 列表（此列表显示在其自身的函数体中执行代码时被大量采样的函数）。  
  
     检查“热路径”**** 列表并注意 PeopleNS.People.GetNames 方法是最靠近该列表末尾的 PeopleTrax 函数。 其位置使其成为进行分析较好的候选。 单击函数名以显示“函数详细信息”**** 视图中 GetNames 的详细信息。  
  
2. “函数详细信息”**** 视图包含两个窗口。 成本分配窗口提供关于函数所执行的工作的图形视图、它调用的函数所执行工作的图形视图以及对被采样的实例数量调用函数的函数分布的图形视图。 可以单击函数名更改作为视图焦点的函数。 例如，可以单击“PeopleNS.People.GetPeople”使 GetPeople 作为所选函数。  
  
     “函数代码视图”**** 窗口显示函数的源代码（如果可用），并突出显示所选函数中最昂贵的行。 选择“GetNames”后，可以看到此函数读取来自应用程序资源的字符串，然后使用 <xref:System.IO.StringReader> 将字符串中的每行添加到 <xref:System.Collections.ArrayList>。 没有明显的方法可优化此函数。  
  
3. 由于 PeopleNS.People.GetPeople 是 GetNames 的唯一调用方，因此可在成本分配窗口中单击“GetPeople”以检查其代码。 此方法会从 GetNames 生成的人员和公司名称中返回 PersonInformationNS.PersonInformation 对象的 <xref:System.Collections.ArrayList>。 但是，每次创建 PersonInformation 对象时，都会调用两次 GetNames。 可以看到，通过在方法开始时仅创建一次列表并在 PersonInformation 创建循环期间并索引编入这些列表，可轻松地优化该方法。  
  
4. GetPeople 的可选版本随附示例应用程序代码，你可以通过将条件编译符号添加到生成属性以调用优化后的函数。 在“解决方案资源管理器”窗口中，右键单击“人员”项目，然后单击“属性”****。 单击属性页菜单上的“生成”****，然后在条件编译符号文本框中键入 **OPTIMIZED_GETPEOPLE**。 GetPeople 的优化版本将替换下一个生成中的原始方法。  
  
5. 重新运行性能会话。 在“性能资源管理器”工具栏上，单击“启动并启用分析功能”****。 单击“获取人员”****，然后单击“导出数据”****。 关闭出现的记事本窗口，然后关闭 People Trax 应用程序。  
  
     将生成新的分析数据文件，并且新数据的“摘要”**** 视图将出现在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 主窗口中。  
  
6. 若要比较两个分析运行，请在“性能资源管理器”中选择两个数据文件，右键单击文件，然后单击“比较性能报告”****。 比较报告窗口将出现在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 主窗口中。 “增量”**** 列显示函数的性能值从早期的“基线”**** 值到后来的“比较”**** 值的变化。 可以从“列”**** 下拉列表中选择要比较的值。 选择“非独占样本数 %”****。  
  
     请注意，GetPeople 和 GetNames 方法显示可观的性能提升。  
  
## <a name="profiling-by-using-the-instrumentation-method"></a>使用检测方法进行分析  
 检测是一种分析方法，在此方法中探查器将探测函数插入到被分析二进制文件的特殊生成的版本中。 探测收集被检测模块中函数进入和退出时以及这些函数中所有调用站点中的计时信息。 检测过程对调查与输入/输出操作相关的问题十分有用，例如写入到磁盘和通过网络进行通信。 检测比采样提供更详细的信息，但它在进程执行中更具侵入性，并导致更多的开销。 被检测的二进制文件也大于调试或发布二进制文件，并且不适用于部署。  
  
 在演练的本部分中，我们将使用检测方法来发现更多可在之前分析的 PeopleTrax 应用程序中优化的代码。 通过使用“摘要”视图时间线的筛选器，我们可将分析重点放在被分析应用程序的导出数据方案上，其中，人员列表被写入到记事本文件中。  
  
#### <a name="to-profile-an-existing-application-by-using-the-instrumentation-method"></a>使用检测方法分析现有应用程序  
  
1. 如有必要，请在 Visual Studio 中打开 PeopleTrax 应用程序。  
  
     请确保以管理员身份运行并且已将该解决方案的生成配置设置为“发布”****。  
  
2. 在“性能资源管理器”中，单击“检测”****。  
  
3. 在“性能资源管理器”工具栏上，单击“启动并启用分析功能”****。  
  
     探查器将生成项目并开始分析应用程序。 将出现 PeopleTrax 应用程序窗口。  
  
4. 单击“获取人员”****。  
  
     PeopleTrax 数据网格将使用数据填充。  
  
5. 等待约 10 秒，然后单击“导出数据”****。  
  
     **记事本**将启动并显示其中包含 PeopleTrax 中的人员列表的新文件。 等待期间，可以更轻松地识别筛选的数据导出过程。  
  
6. 关闭 **记事本**，然后关闭 **PeopleTrax** 应用程序。  
  
     [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 将生成性能会话报表 (*.vsp)。  
  
#### <a name="to-analyze-instrumented-profiling-results"></a>分析检测的分析结果  
  
1. 报表的“摘要”**** 视图的时间线关系图显示分析运行期间该程序的 CPU 使用率。 导出数据操作应为该关系图右侧较大的峰值或停滞。 我们可以筛选性能会话以仅显示和分析导出操作中收集的数据。 单击该关系图上导出数据操作开始的数据点的左侧。 再次单击该操作的右侧。 然后在时间线右侧的链接列表中单击“按选定内容筛选”****。  
  
    “热路径”**** 树显示出 PeopleTrax.Form1.ExportData 方法调用的 <xref:System.String.Concat%2A> 方法消耗的时间占有很大的比重。 由于 **System.String.Concat** 也位于“执行单个工作最多的函数”**** 列表的顶部，因此函数中消耗的时间可能是优化的一个方法。  
  
2. 双击任一摘要表中的“System.String.Concat”**** 以在“函数详细信息”视图中查看更多信息。  
  
3. 可以看到，PeopleTrax.Form1.ExportData 是唯一调用 Concat 的方法。 在“调用函数”**** 列表中单击“PeopleTrax.Form1.ExportData”**** 以选择方法作为“函数详细信息”视图的目标。  
  
4. 在“函数代码视图”窗口中检查该方法。 请注意，没有针对 **System.String.Concat** 的任何文本调用。 相反，多次使用了 += 操作数，编译器将其替换为对 **System.String.Concat** 的调用。 对 .NET Framework 中的字符串进行任何修改都会导致分配一个新的字符串。 .NET Framework 包括针对字符串串联优化的 <xref:System.Text.StringBuilder> 类  
  
5. 若要使用优化后的代码替换此问题区域，请将 OPTIMIZED_EXPORTDATA 作为条件编译符号添加到 PeopleTrax 项目中。  
  
6. 在“解决方案资源管理器”中右键单击 PeopleTrax 项目，再单击“属性”****。  
  
    将出现 PeopleTrax 项目属性窗体。  
  
7. 单击“生成”**** 选项卡。  
  
8. 在“条件编译符号”**** 文本框中，键入 **OPTIMIZED_EXPORTDATA**。  
  
9. 关闭项目属性窗体，然后在系统提示时选择“保存全部”****。  
  
   再次运行应用程序时，你将看到性能有了显著的改进。 建议即使有了用户可见的性能改进，也再次运行性能分析会话。 有必要在修复问题后查看数据，因为第一个问题可能掩盖某些其他问题。  
  
## <a name="see-also"></a>另请参阅  
 [概述](../profiling/overviews-performance-tools.md)   
 [入门](../profiling/getting-started-with-performance-tools.md)   
 [/Z7、/Zi、/ZI (调试信息格式) ](https://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8)
