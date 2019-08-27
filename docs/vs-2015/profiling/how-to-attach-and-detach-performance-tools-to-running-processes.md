---
title: 如何：附加和分离性能工具正在运行的进程 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.attach
helpviewer_keywords:
- performance tools, attach process
- profiling tools, detach process
- profiling tools, attach process
- performance tools, detach process
- profiler
ms.assetid: 56a99c39-e7f6-4f48-ae56-04ab8e022bf7
caps.latest.revision: 35
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0b8fc664ee47cd34ab984d1ac448b45c2f17c5b0
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443710"
---
# <a name="how-to-attach-and-detach-performance-tools-to-running-processes"></a>如何：附加和分离性能工具正在运行的进程
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

探查器可用于附加到运行中的进程或从运行中的进程分离，以更轻松地进行采样和收集性能数据。 在想要避免收集有关应用程序加载时间的数据，或在进程达到某一特定状态后监视其性能时，可使用此方法分析进程。  
  
> [!NOTE]
> 以下步骤适用于在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 集成开发环境 (IDE) 中附加进程或从中分离进程。 有关如何使用命令行工具的信息，请参阅[从命令行分析](../profiling/using-the-profiling-tools-from-the-command-line.md)。 有关如何分析服务的信息，请参阅[分析服务](../profiling/command-line-profiling-of-services.md)。  
  
 可用于分析的进程取决于计算机管理员所设置的用户访问权限。 例如，用户帐户可能具有下列任一权限：  
  
- 当管理员启动了驱动程序和服务时，可访问高级分析功能。  
  
- 仅可访问样本分析（域用户）。  
  
- 拒绝所有人访问分析。  
  
  有关详细信息，请参阅[分析和 Windows Vista 安全性](../profiling/profiling-and-windows-vista-security.md)和 [VSPerfCmd](../profiling/vsperfcmd.md) 中的管理选项。  
  
### <a name="to-attach-to-a-running-process"></a>附加到正在运行的进程  
  
1. 在“分析”菜单上，指向“探查器”，然后单击“附加/分离”。  
  
     \- 或 -  
  
     在“性能资源管理器”中，右键单击性能会话，然后单击“附加/分离”。  
  
     将出现“将探查器附加到进程”对话框。  
  
2. 单击要附加到的进程的名称。  
  
3. 单击 **“附加”**。  
  
### <a name="to-detach-from-a-running-process"></a>从运行中的进程分离  
  
1. 在“分析”菜单上，指向“探查器”，然后单击“附加/分离”。  
  
     \- 或 -  
  
     在“性能资源管理器”中，右键单击性能会话，然后单击“附加/分离”。  
  
     将出现“将探查器附加到进程”对话框。  
  
2. 单击要从中分离的映像名称。  
  
3. 单击“分离”。  
  
## <a name="see-also"></a>请参阅  
 [控制数据收集](../profiling/controlling-data-collection.md)   
 [性能会话概述](../profiling/performance-session-overview.md)   
 [如何：开始和结束性能数据收集](../profiling/how-to-start-and-end-performance-data-collection.md)   
 [分析和 Windows Vista 安全性](../profiling/profiling-and-windows-vista-security.md)   
 [VSPerfCmd](../profiling/vsperfcmd.md)
