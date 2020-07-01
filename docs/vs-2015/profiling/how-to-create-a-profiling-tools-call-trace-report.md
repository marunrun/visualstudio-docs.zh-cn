---
title: 如何：创建分析工具调用跟踪报表 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- performance tools, viewing ETW data
- ETW [Visual Studio ALM], viewing data
ms.assetid: 7640520a-7d3c-456c-b184-872a5d2f82f3
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fbf92b38f9408455e10048fbd4a5e84fdf822ea2
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547987"
---
# <a name="how-to-create-a-profiling-tools-call-trace-report"></a>如何：创建分析工具调用跟踪报告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 分析工具的调用跟踪报告  将列出应用程序函数每个入口点和出口点的计时信息，以及该函数对其他函数的每次调用的计时信息。 仅当使用检测方法收集时，调用跟踪报告才可用于分析数据。  
  
> [!NOTE]
> 不能在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中显示调用跟踪报告。 必须使用**VSPerfReport**命令行工具才能生成逗号分隔值（.csv）或 Xml 文件。 有关此工具的详细信息，请参阅 [VSPerfReport](../profiling/vsperfreport.md)。  
  
### <a name="to-create-a-call-trace-report"></a>创建调用跟踪报告  
  
1. 打开“命令提示符”**** 窗口。  
  
2. 在命令提示符处，键入下列命令：  
  
     *ToolsPath* **VSPerfReport** *VSPFile*  **/CallTrace [/Xml]**  
  
    |Command 元素|说明|
    |-|-|  
    |*ToolsPath*|分析工具命令行工具的路径。 有关详细信息，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。|  
    |*VSPFile*|分析数据（.vsp 或 .vsps）文件。 接受完整和部分路径。|  
    |Xml|生成 Xml 格式的报告。|  
  
## <a name="see-also"></a>另请参阅  
 [如何：收集 Windows 事件跟踪（ETW）数据](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)   
 [分析工具 API](../profiling/profiling-tools-apis.md)
