---
title: 演练：使用检测进行命令行分析 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, walkthroughs
- performance tools, walkthroughs
- performance tools, command-line tools
ms.assetid: 1c6f1586-3d6a-431f-bedf-c54088e280ba
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3a37350cf274fbb551326ac96387330b0f3956e7
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63439701"
---
# <a name="walkthrough-command-line-profiling-using-instrumentation"></a>演练：命令行使用检测进行分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练将演示通过使用分析工具的检测方法分析 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 独立应用程序以收集详细的计时和调用计数数据。 在本演练中，你将完成以下任务：  
  
- 使用 [VSInstr](../profiling/vsinstr.md) 命令行工具生成被检测的二进制文件。  
  
- 使用 [VSPerfCLREnv](../profiling/vsperfclrenv.md) 工具设置环境变量以收集 .NET 分析数据。  
  
- 使用 [VSPerfCmd](../profiling/vsperfcmd.md) 工具收集分析数据。  
  
- 使用 [VSPerfReport](../profiling/vsperfreport.md) 工具生成基于文件的分析数据的报告。  
  
## <a name="prerequisites"></a>系统必备  
  
- [!INCLUDE[vsprvsts](../includes/vsprvsts-md.md)]  
  
- 对 C# 有中等程度的理解  
  
- 对命令行工具的使用有中等程度的理解  
  
- [PeopleTrax 示例](../profiling/peopletrax-sample-profiling-tools.md)的副本  
  
- 若要使用分析提供的信息，最好有可用的调试符号信息。 有关详细信息，请参阅[如何：引用 Windows 符号信息](../profiling/how-to-reference-windows-symbol-information.md)。  
  
## <a name="command-line-profiling-using-the-instrumentation-method"></a>使用检测方法进行命令行分析  
 检测是一种分析方法，通过它，被检测二进制文件的特别生成的版本中将包含可在被监测模块中收集函数进入和退出时的计时信息的探测函数。 由于这种分析方法比采样更具侵入性，因此将导致更多的开销。 被检测的二进制文件也大于调试或发布二进制文件，并且不适用于部署。  
  
> [!NOTE]
> 请勿向客户发送被检测的二进制文件。 被检测的二进制文件可能具有多种风险。 这些二进制文件包含使应用程序更容易反向工程以及安全性风险的信息。  
  
#### <a name="to-profile-the-peopletrax-application-by-using-the-instrumentation-method"></a>使用检测方法分析 PeopleTrax 应用程序  
  
1. 安装 PeopleTrax 示例应用程序并生成发布版本。  
  
2. 打开命令提示符窗口，然后向本地路径环境变量添加**分析工具**目录。  
  
3. 将工作目录更改为包含 PeopleTrax 二进制文件的目录。  
  
4. 创建目录以包含基于文件的报表。 键入以下命令：  
  
    ```  
    md Reports  
    ```  
  
5. 将 VSInstr 命令行工具用于检测应用程序中的二进制文件。 在单独的命令行上键入以下命令：  
  
    ```  
    VSInstr PeopleTrax.exe  
    VSInstr PeopleTrax.exe  
    VSInstr People.dll  
    VSInstr Person.dll  
    VSInstr Operation.dll  
    ```  
  
     **请注意**：默认情况下，VSInstr 将保存原始文件的非检测备份。 备份文件的扩展名为 .orig。 例如，“MyApp.exe”的原始版本将另存为“MyApp.exe.orig”。  
  
6. 键入以下命令设置相应的环境变量：  
  
    ```  
    VsPerfCLREnv /traceon  
    ```  
  
7. 若要启动探查器，请键入以下命令：  
  
    ```  
    VsPerfCmd /start:trace /output:Reports\Report.vsp  
    ```  
  
8. 在跟踪模式下启动探查器后，请运行 PeopleTrax.exe 进程的被检测版本以收集数据。  
  
     将出现“PeopleTrax”应用程序窗口。  
  
9. 单击“获取人员”。  
  
     PeopleTrax 数据网格将使用数据填充。  
  
10. 单击“导出数据”。  
  
     记事本将启动并显示其中包含 **PeopleTrax** 应用程序中的人员列表的新文件。  
  
11. 关闭记事本，然后关闭 **PeopleTrax** 应用程序。  
  
12. 关闭探查器。 键入以下命令：  
  
    ```  
    VSPerfCmd /shutdown  
    ```  
  
13. 键入以下命令重置环境变量：  
  
    ```  
    VSPerfCLREnv /off  
    ```  
  
14. 使用 VSPerfReport 工具生成逗号分隔值 (.csv) 报表文件。 类型:  
  
    ```  
    VSPerfReport Reports\Report.vsp /output:Reports /summary:all  
    ```  
  
     可以在电子表格程序中分析生成的报表，也可以使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE 分析 Report.vsp 文件中的分析数据。 有关详细信息，请参阅[分析性能工具数据](../profiling/analyzing-performance-tools-data.md)。  
  
## <a name="see-also"></a>请参阅  
 [性能会话概述](../profiling/performance-session-overview.md)   
 [从命令行分析](../profiling/using-the-profiling-tools-from-the-command-line.md)   
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [了解采样数据值](../profiling/understanding-sampling-data-values.md)   
 [性能报告视图](../profiling/performance-report-views.md)
