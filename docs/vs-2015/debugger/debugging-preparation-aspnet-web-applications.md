---
title: 调试准备： ASP.NET Web 应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- VB
- CSharp
helpviewer_keywords:
- debugging ASP.NET Web applications
- debugging [Visual Studio], Web applications
ms.assetid: bcfb1080-98d1-42f9-96af-186fb14f232a
caps.latest.revision: 38
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7a80587062442688551d07128a2cec49a712adf6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65691464"
---
# <a name="debugging-preparation-aspnet-web-applications"></a>调试准备：ASP.NET Web 应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

网站 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 模板创建 Web 窗体应用程序。 当你使用此模板创建网站时，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 会创建用于调试的默认设置。 在 " **项目属性** " 对话框中，您可以指定是否希望网页成为启动页面。 当你开始 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 使用这些默认设置调试网站时，将 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 启动 Internet Explorer，并将调试器附加到 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 工作进程 ( # A0 或 w3wp.exe) 。 有关详细信息，请参阅 [System Requirements](../debugger/aspnet-debugging-system-requirements.md)。  
  
### <a name="to-create-a-web-forms-application"></a>创建 Web 窗体应用程序  
  
1. 在 " **文件** " 菜单上，选择 " **新建**网站"。  
  
2. 在 "**新建**网站" 对话框中，选择 "网站" [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] **Web Site**。  
  
3. 单击“确定”。  
  
### <a name="to-debug-your-web-form"></a>调试 Web 窗体  
  
1. 在您的函数和事件处理程序中设置一个或多个断点。  
  
     有关详细信息，请参阅 [Breakpoints and Tracepoints](https://msdn.microsoft.com/fe4eedc1-71aa-4928-962f-0912c334d583)。  
  
2. 命中断点时，逐句通过函数内的代码。 同时观察代码的执行，直到将问题隔离出来。  
  
     有关详细信息，请参阅 [单步执行](https://msdn.microsoft.com/8791dac9-64d1-4bb9-b59e-8d59af1833f9) 和 [调试 Web 应用程序和脚本](../debugger/debugging-web-applications-and-script.md)。  
  
## <a name="changing-default-configurations"></a>更改默认配置  
 如果需要更改 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 创建的默认的调试和发布配置，则可以这样做。 有关详细信息，请参阅[如何：设置调试和发布配置](../debugger/how-to-set-debug-and-release-configurations.md)。  
  
#### <a name="to-change-the-default-debug-configuration"></a>更改默认的调试配置  
  
1. 在 **解决方案资源管理器**中，右键单击该网站，然后选择 " **属性页** " 以打开 " **属性页** " 对话框。  
  
2. 单击 " **启动选项**"。  
  
3. 将 " **启动操作** " 设置为应该首先显示的网页。  
  
4. 在 " **调试器**" 下，确保已选择 " **ASP.NET 调试** "。  
  
     有关详细信息，请参阅 [Web 项目的属性页设置](../debugger/property-pages-settings-for-web-projects.md)。  
  
## <a name="see-also"></a>另请参阅  
 [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)   
 [调试器基础知识](../debugger/debugger-basics.md)   
 [调试器安全性](../debugger/debugger-security.md)   
 [调试托管代码](../debugger/debugging-managed-code.md)
