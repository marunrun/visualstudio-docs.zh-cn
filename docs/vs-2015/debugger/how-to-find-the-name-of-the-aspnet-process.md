---
title: 如何：查找 ASP.NET 进程的名称 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- ASP.NET debugging, ASP.NET process
- ASP.NET process
ms.assetid: 931a7597-b0f0-4a28-931d-46e63344435f
caps.latest.revision: 32
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 53072013c1665687262d30f4a0c2720641c920be
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65685967"
---
# <a name="how-to-find-the-name-of-the-aspnet-process"></a>如何：查找 ASP.NET 进程的名称
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要附加到正在运行的 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 应用程序，您必须知道 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 进程的名称：  
  
- 如果正在运行 IIS 6.0 或 IIS 7.0，则名称为 w3wp.exe。  
  
- 如果正在运行 IIS 的早期版本，则该进程的名称为 aspnet_wp.exe。  
  
  对于使用 [!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)] 或更高版本生成的应用程序， [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 代码可驻留在文件系统上并在测试服务器 WebDev.WebServer.exe 下运行。 在这种情况下，必须附加到 WebDev.WebServer.exe 而不是 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 进程。 此方案仅适用于本地调试。  
  
  当原来的 ASP 应用程序在进程内运行时，它们会在 IIS 进程 inetinfo.exe 内部运行。  
  
> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### <a name="to-determine-whether-project-code-resides-on-the-file-system-or-iis"></a>确定项目代码驻留在文件系统上还是 IIS 上  
  
1. 在 Visual Studio 中，打开 **解决方案资源管理器** （如果尚未打开）。  
  
2. 选择包含该应用程序名称的顶部节点。  
  
3. 如果 " **属性** " 窗口标题包含文件路径，则应用程序代码驻留在文件系统上。  
  
     否则，" **属性** " 窗口标题将包含网站的名称。  
  
### <a name="to-determine-the-iis-version-under-which-the-application-is-running"></a>确定应用程序正在哪个 IIS 版本下运行  
  
1. 查找 " **管理工具** " 并运行它。 根据您的操作系统，这可能是 **控制面板**中的图标，或单击 " **启动**" 时显示的菜单项。  
  
     在 Windows XP 中， **"控制面板"** 可以在 "类别" 视图或 "经典" 视图中。 在类别视图中，必须单击 " **切换到经典视图** " 或 " **性能和维护** " 才能看到 " **管理工具** " 图标。  
  
2. 从 " **管理工具**" 中，运行 Internet Information Services。 将出现一个 MMC 对话框。  
  
3. 如果左侧窗格中列出了多个计算机，请选择驻留了该应用程序代码的那个计算机。  
  
4. IIS 版本位于右窗格的 " **版本** " 列中。  
  
## <a name="see-also"></a>另请参阅  
 [远程调试 Web 应用程序的先决条件](../debugger/prerequistes-for-remote-debugging-web-applications.md)   
 [系统要求](../debugger/aspnet-debugging-system-requirements.md)   
 [准备调试 ASP.NET](../debugger/preparing-to-debug-aspnet.md)   
 [调试 Web 应用程序和脚本](../debugger/debugging-web-applications-and-script.md)
