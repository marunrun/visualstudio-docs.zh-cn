---
title: 使用 VSPerfASPNETCmd 进行快速网站分析 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- proflilng tools,VSPerfASPNETCmd
- VSPerfASPNETCmd
ms.assetid: 9a9d62a6-549a-45ac-a948-76eb98586ac5
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5ce5534f5723a3f0e570779939f207018cac71cd
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438908"
---
# <a name="rapid-web-site-profiling-with-vsperfaspnetcmd"></a>使用 VSPerfASPNETCmd 进行快速网站分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过 **VSPerfASPNETCmd** 命令行工具可以轻松地分析 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web 应用程序。 与 [VSPerfCmd](../profiling/vsperfcmd.md) 命令行工具相比，减少了选项、不必设置任何环境变量以及无需重启计算机。 使用 **VSPerfASPNETCmd** 是使用独立探查器进行分析时的首选方法。 有关详细信息，请参阅[如何：安装独立 Profiler](../profiling/how-to-install-the-stand-alone-profiler.md)。  
  
> [!NOTE]
> Windows 8 和 Windows Server 2012 中增强的安全功能需要以 Visual Studio 探查器在这些平台上收集数据的方式进行重大更改。 Windows 应用商店应用程序也需要新的收集技术。 请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。  
  
 在某些情况下（如收集并发数据或暂停并恢复分析），使用 **VSPerfCmd** 是首选分析方法。  
  
> [!NOTE]
> 分析工具的命令行工具位于 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 安装目录的 \Team Tools\Performance Tools 子目录中。 在 64 位计算机，使用位于 32 位 \Team Tools\Performance Tools 目录中的 VSPerfASPNETCmd 工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。 有关详细信息，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。  
  
## <a name="profiling-an-aspnet-application"></a>分析 ASP.NET 应用程序  
 若要分析 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web 应用程序中，请输入以下各节所述的命令之一。 网站会启动且探查器会开始收集数据。 执行应用程序，然后关闭浏览器。 若要停止分析，请在命令提示符窗口中按 Enter 键。  
  
> [!NOTE]
> 默认情况下，在执行 **vsperfaspnetcmd** 命令之后，命令提示符不会返回。 可以使用 **/nowait** 选项强制命令提示符返回。 请参阅[使用 /NoWait 选项](#UsingNoWait)。  
  
## <a name="to-collect-application-statistics-by-using-the-sampling-method"></a>使用采样方法收集应用程序统计信息  
 采样是 **VSPerfASPNETCmd** 工具的默认分析方法，不必在命令行上指定。 以下命令行从指定 Web 应用程序收集应用程序统计信息：  
  
 **vsperfaspnetcmd**  *websiteUrl*  
  
## <a name="to-collect-detailed-timing-data-by-using-the-instrumentation-method"></a>使用检测方法收集详细计时数据  
 使用以下命令行可从动态编译的 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web 应用程序收集详细计时数据：  
  
 **vsperfaspnetcmd /trace**  *websiteUrl*  
  
 如果要分析 Web 应用程序中的静态编译的 .dll 文件，则必须使用 [VSInstr](../profiling/vsinstr.md) 命令行工具检测文件。 vsperfaspnetcmd /trace 命令会包含检测的文件中的数据。  
  
## <a name="to-collect-net-memory-data"></a>收集 .NET 内存数据  
 **/Memory** 选项会收集有关 .NET 内存中的对象分配的数据，并且可以收集有关这些对象的生存期的数据。 分配数据收集是 **/Memory** 数据选项的默认模式，不必在命令行上指定。  
  
 **vsperfaspnetcmd /memory** *websiteUrl*  
  
 使用 **Lifetime** 参数可收集对象生存期数据以及分配数据：  
  
 **vsperfaspnetcmd /memory:lifetime** *websiteUrl*  
  
 还可以使用 **/Trace** 选项包含详细计时信息及 .NET 内存数据：  
  
 **vsperfaspnetcmd /memory**[ **:lifetime**] **/trace**`websiteUrl`  
  
## <a name="to-collect-tier-interaction-data"></a>收集层交互数据  
  
> [!WARNING]
> 可以使用 [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]、[!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] 或 [!INCLUDE[vs_pro_current_short](../includes/vs-pro-current-short-md.md)] 收集层交互分析 (TIP) 数据。 但是，层交互分析数据只能在 [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)] 和 [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]中查看。  
>   
> 若要收集有关 Windows 8 或 Windows Server 2012 的 TIP 数据，必须使用检测 (/trace  ) 选项。  
  
 随采样数据收集层交互数据：  
  
 **vsperfaspnetcmd /tip** `websiteUrl`  
  
 随检测数据收集层交互数据：  
  
 **vsperfaspnetcmd /trace /tip** *websiteUrl*  
  
 随 .NET 内存数据收集层交互数据：  
  
 **vsperfaspnetcmd /memory**[ **:lifetime**] **/tip**_websiteUrl_  
  
## <a name="UsingNoWait"></a> 使用 /NoWait 选项  
 默认情况下，在执行 **vsperfaspnetcmd** 命令之后，命令提示符不会返回。 可以使用以下语法选项强制命令提示符返回。 随后可以在命令提示符窗口中执行其他操作。 若要结束分析，请在单独的 **vsperfaspnetcmd** 命令中使用 **/shutdown** 选项。  
  
 开始分析：  
  
 **vsperfaspnetcmd** [ */Options*] **/nowait**_websiteUrl_  
  
 结束分析：  
  
 **vsperfaspnetcmd /shutdown** *websiteUrl*  
  
## <a name="additional-options"></a>附加选项  
 可以将以下任何选项添加到本节前面列出的命令（**vsperfaspnetcmd /shutdown** 命令除外）。  
  
|选项|描述|  
|------------|-----------------|  
|**/Output:** `VspFile`|默认情况下，在当前目录中创建分析数据 (.vsp) 文件，文件名为 **PerformanceReport.vsp**。 使用 /Output 选项可指定其他位置、文件名或两者。|  
|**/PackSymbols:Off**|VsPerfASPNETCmd 会将符号（函数和参数名等）嵌入在 .vsp 文件中。 嵌入符号可能会使分析数据文件非常大。 如果在分析数据时可以访问包含符号的 .pdb 文件，则使用 /packsymbols:off 选项禁用符号的嵌入。|
