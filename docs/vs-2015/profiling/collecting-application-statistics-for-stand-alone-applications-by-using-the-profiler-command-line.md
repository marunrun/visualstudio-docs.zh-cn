---
title: 使用探查器命令行收集独立应用程序的应用程序统计信息 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- sampling profiling method
- profilng tools,sampling method
ms.assetid: be2dbdd0-fc88-45f9-a1d5-bcb4f64e17ad
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 03e27d021b8b3c5ec29a8646a1bbe7bc6ebdecc0
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63441299"
---
# <a name="collecting-application-statistics-for-stand-alone-applications-by-using-the-profiler-command-line"></a>使用探查器命令行收集独立应用程序的统计信息
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本部分介绍从命令行使用采样方法收集客户端（独立）应用程序的性能统计信息的步骤和选项。  
  
> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 Windows 应用商店应用程序也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。  
  
## <a name="common-tasks"></a>常规任务  
  
|任务|相关的内容|  
|----------|---------------------|  
|**使用分析启动应用程序**|-   [如何：启动独立应用程序，并收集应用程序统计信息](../profiling/how-to-launch-a-stand-alone-application-with-the-profiler-and-collect-application-statistics-by-using-the-command-line.md)|  
|**将探查器附加到正在运行的 .NET Framework 应用程序**|-   [如何：将探查器附加到 .NET Framework 应用程序，并收集应用程序统计信息](../profiling/how-to-attach-the-profiler-to-a-dotnet-framework-stand-alone-application-and-collect-application-statistics-by-using-the-command-line.md)|  
|**将探查器附加到正在运行的 C/C++ 应用程序**|-   [如何：将探查器附加到本机应用程序，并收集应用程序统计信息](../profiling/how-to-attach-the-profiler-to-a-native-stand-alone-application-and-collect-application-statistics-by-using-the-command-line.md)|  
|**添加层交互数据**|-   [收集层交互数据](../profiling/adding-tier-interaction-data-from-the-command-line.md)|  
  
## <a name="related-tasks"></a>相关任务  
  
### <a name="profiling-stand-alone-applications"></a>分析独立应用程序  
  
|任务|相关的内容|  
|----------|---------------------|  
|**检测应用程序**|-   [使用检测收集详细计时数据](../profiling/collecting-detailed-timing-data-for-a-stand-alone-application-by-using-the-profiler-command-line.md)|  
|**收集 .NET 内存分配和垃圾回收数据**|-   [收集 .NET Framework 内存数据](../profiling/collecting-dotnet-framework-memory-data-for-stand-alone-applications-by-using-the-profiler-command-line.md)|  
|**收集资源争用和线程执行数据**|-   [收集并发数据](../profiling/collecting-concurrency-data-for-stand-alone-applications-by-using-the-profiler-command-line.md)|  
  
### <a name="profiling-by-using-the-sampling-method"></a>使用采样方法进行分析  
  
|任务|相关的内容|  
|----------|---------------------|  
|**分析 ASP.NET Web 应用程序**|-   [使用采样法收集应用程序统计信息](/visualstudio/profiling/collecting-concurrency-data-for-an-aspnet-web-application?view=vs-2015)|  
|**分析服务**|-   [使用采样法收集应用程序统计信息](../profiling/collecting-application-statistics-for-services-by-using-the-profiler-sampling-method.md)。 介绍如何使用采样方法收集 Windows 服务的性能统计信息。|  
  
### <a name="analyzing-sampling-data-views-and-reports"></a>分析采样数据视图和报告  
 [采样方法数据视图](../profiling/profiler-sampling-method-data-views.md)
