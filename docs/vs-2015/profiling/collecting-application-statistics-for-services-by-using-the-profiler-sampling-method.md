---
title: 使用探查器采样法收集服务的应用程序统计信息 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 07840ab2-3a92-4744-ac87-48b19e0ceecd
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f3f556a039ab131a563a90010112009b39f4c981
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63445748"
---
# <a name="collecting-application-statistics-for-services-by-using-the-profiler-sampling-method"></a>使用探查器采样方法收集服务的应用程序统计信息
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本部分介绍从命令行使用采样方法收集 Windows 服务的性能统计信息的步骤和选项。  
  
> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 Windows 应用商店应用程序也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。  
  
## <a name="common-tasks"></a>常规任务  
  
|任务|相关内容|  
|----------|---------------------|  
|**将探查器附加到 .NET 服务**|-   [如何：将探查器附加到 .NET 服务以收集应用程序统计信息](../profiling/how-to-attach-the-profiler-to-a-dotnet-service-to-collect-application-statistics-by-using-the-command-line.md)|  
|**添加层交互数据**|-   [收集层交互数据](../profiling/adding-tier-interaction-data-from-the-command-line.md)|  
|**将探查器附加到 C/C++ 服务**|-   [如何：将探查器附加到本机服务以收集应用程序统计信息](../profiling/how-to-attach-the-profiler-to-a-native-service-to-collect-application-statistics-by-using-the-command-line.md)|  
  
## <a name="related-tasks"></a>相关任务  
  
### <a name="profiling-windows-services"></a>分析 Windows 服务  
  
|任务|相关内容|  
|----------|---------------------|  
|**使用检测方法进行分析**|-   [使用检测收集详细计时数据](../profiling/collecting-detailed-timing-data-for-services-by-using-the-instrumentation-method-from-the-profiler-command-line.md)|  
|**分析 .NET 内存分配和垃圾回收**|-   [收集 .NET 内存数据](../profiling/collecting-memory-data-from-dotnet-framework-services-by-using-the-profiler-command-line.md)|  
|**分析资源争用和线程活动**|-   [收集并发数据](../profiling/collecting-concurrency-data-for-a-service-by-using-the-profiler-command-line.md)|  
  
### <a name="profiling-by-using-the-sampling-method"></a>使用采样方法进行分析  
  
|任务|相关内容|  
|----------|---------------------|  
|**分析独立（客户端）应用程序**|-   [使用采样法收集应用程序统计信息](../profiling/collecting-application-statistics-for-stand-alone-applications-by-using-the-profiler-command-line.md)|  
|**分析 ASP.NET Web 应用程序**|-   [使用采样法收集应用程序统计信息](/visualstudio/profiling/collecting-concurrency-data-for-an-aspnet-web-application?view=vs-2015)|  
  
### <a name="analyzing-sampling-data-views-and-reports"></a>分析采样数据视图和报告  
 [采样方法数据视图](../profiling/profiler-sampling-method-data-views.md)
