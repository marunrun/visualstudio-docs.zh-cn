---
title: VSPerf | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: b5854e62-279e-4850-bfeb-0c6ef82f4805
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a8042b228a481dc3d720d8b422963db41abbddcd
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533830"
---
# <a name="vsperf"></a>VSPerf
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 **VsPerf** 命令行工具可以：  
  
1. 在设备上未安装 Visual Studio 时，从命令行分析 Windows 应用商店应用。  
  
2. 使用采样分析方法分析 Windows 8 桌面应用程序和 Windows Server 2012 应用程序。  
  
   有关分析选项的详细信息，请参阅 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)。  
  
## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> 在本主题中  
 本主题描述了可与 `vsperf.exe` 命令行工具一起使用的选项。 本主题包含以下各节：  
  
 [仅限 Windows 应用商店应用](#BKMK_windows_store_apps_only)  
  
 [仅限 Windows 8 桌面应用程序和 Windows Server 2012 应用程序](#BKMK_Windows_8_classic_applications_and_Windows_Server_2012_applications_only)  
  
 [所有应用程序](#BKMK_All_applications)  
  
## <a name="windows-store-apps-only"></a><a name="BKMK_windows_store_apps_only"></a>仅限 Windows 应用商店应用  
 这些选项仅适用于 Windows 应用商店应用。  
  
|选项|说明|  
|-|-|  
|**/app:{AppName}**|启动探查器，然后等待指定的应用从“开始”菜单中启动。<br /><br /> 运行 `vsperf /listapps` 以查看应用名称和已安装应用的 PackageFullName。|  
|**/package:{PackageFullName}**|启动探查器，然后等待指定的应用从“开始”菜单中启动。<br /><br /> 运行 `vsperf /listapps` 以查看应用名称和已安装应用的 PackageFullName。|  
|**可通过/js**|分析 JavaScript 应用所必需的。<br /><br /> 从 JavaScript 应用中收集性能数据。<br /><br /> 仅与 /package 或 /attach 一起使用。|  
|**/noclr**|可选。 不收集 CLR 数据。<br /><br /> 仅与 /package 或 /attach 一起使用。<br /><br /> 优化，不会解析任何托管符号。|  
|**/listapps**|列出已安装的应用名称和 PackageFullNames。|  
  
## <a name="windows-8-desktop-applications-and-windows-server-2012-applications-only"></a><a name="BKMK_Windows_8_classic_applications_and_Windows_Server_2012_applications_only"></a>仅限 windows 8 桌面应用程序和 Windows Server 2012 应用程序  
 这些选项不适用于 Windows 应用商店应用。  
  
|选项|说明|  
|-|-|  
|**/launch： {Executable}**|启动并开始分析指定的可执行文件。|  
|**/args:{ExecutableArguments}**|指定要传递 **/launch** 目标的命令行参数。|  
|**/console**|在新的命令窗口中运行 **/launch** 目标。|  
  
## <a name="all-applications"></a><a name="BKMK_All_applications"></a>所有应用程序  
 这些选项适用于任何 Windows 8 或 Windows Server 2012 应用程序。  
  
|选项|说明|  
|-|-|  
|**/attach:{PID&#124;ProcessName}[,PID&#124;ProcessName]...**|从指定的进程收集数据。<br /><br /> 使用任务管理器查看正在运行的应用的进程 ID (PID) 和进程名称。|  
|**/file:{ReportName}**|可选。 指定输出文件（将覆盖现有文件）。<br /><br /> 仅与 /package 或 /attach 一起使用。|  
|**/pause**|暂停数据收集。|  
|**/resume**|恢复数据收集。|  
|**/stop**|停止数据收集并终止目标进程。|  
|**/detach**|停止数据收集，但允许目标进程继续运行。|  
|**/status**|显示探查器状态。|  
  
## <a name="see-also"></a>另请参阅  
 [Windows 8 和 Windows Server 2012 应用程序上的性能工具](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)   
 [通过命令行进行分析](../profiling/using-the-profiling-tools-from-the-command-line.md)
