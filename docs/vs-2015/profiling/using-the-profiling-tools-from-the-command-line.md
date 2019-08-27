---
title: 从命令行使用分析工具 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- command line, performance tools
- command-line tools, performance tools
- profiling tools,command line
- tools, command-line
- command line, tools
ms.assetid: 6593fa82-181e-4009-a0ed-02aa24c2c063
caps.latest.revision: 40
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ebd0fbabb73d4c77d1d888b207882e7403f46aab
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431621"
---
# <a name="using-the-profiling-tools-from-the-command-line"></a>从命令行使用分析工具
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 分析工具的命令行工具在命令提示符处分析应用程序，以及使用批处理文件和脚本自动执行分析。 还可以在命令提示符处生成报告文件。 可以使用轻量级独立探查器在未安装 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的计算机上收集数据。  
  
> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 Windows 应用商店应用程序也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。  
  
## <a name="common-tasks"></a>常规任务  
  
|任务|相关内容|  
|----------|---------------------|  
|**设置符号的位置：** 若要显示函数和参数的名称，探查器必须分析的二进制文件的符号 (.pdb) 文件具有访问权限。 这些文件应包括用于 Microsoft 操作系统以及要在分析中查看的应用程序的符号文件。 可以使用公共 Microsoft 符号服务器确保具有用于 Microsoft 二进制文件的正确 .pdb 文件。|-   [如何：通过命令行指定符号文件位置](../profiling/how-to-specify-symbol-file-locations-from-the-command-line.md)|  
|**分析应用程序：** 用于分析目标应用程序的命令行工具和选项取决于应用程序的类型、分析方法以及目标是托管还是本机应用程序。|-   [从命令行使用分析方法](../profiling/using-profiling-methods-to-collect-performance-data-from-the-command-line.md)<br />-   [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)<br />-   [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)<br />-   [分析服务](../profiling/command-line-profiling-of-services.md)|  
|**创建 .xml 和 .csv 报表：** 在命令提示符处进行分析会创建可以在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 界面中查看的数据文件。 还可以使用 VSPerfReport 命令行工具生成数据的 .xml 或逗号分隔值 (.csv) 文件。|-   [从命令行创建探查器报告](../profiling/creating-profiler-reports-from-the-command-line.md)<br />-   [VSPerfReport](../profiling/vsperfreport.md)|  
|**在没有 Visual Studio 的计算机上分析代码：** 可以使用分析工具独立探查器在未安装 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的计算机上为应用程序收集数据。|-   [如何：安装独立探查器](../profiling/how-to-install-the-stand-alone-profiler.md)|  
  
## <a name="reference"></a>参考  
 [命令行分析工具参考](../profiling/command-line-profiling-tools-reference.md)  
  
## <a name="see-also"></a>请参阅  
 [性能资源管理器](../profiling/performance-explorer.md)
