---
title: 如何：调试 Web 应用程序 |Microsoft Docs
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
- Web services, debugging
- ASP.NET Web Forms, debugging
- ASP.NET, debugging Web applications
- debugging ASP.NET Web applications, during development
ms.assetid: 6440d12e-6b29-42c5-a958-99aeaaff480f
caps.latest.revision: 40
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cd3cbbcd740c0f124b8ab4379204a9d425cd541c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205402"
---
# <a name="how-to-debug-web-applications"></a>如何：调试 Web 应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 是在中开发 Web 应用程序的主要技术 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 调试器为在本地或远程服务器上调试 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web 应用程序提供了强大的工具。 本主题介绍如何 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 在开发期间调试项目。 有关如何调试 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 已部署到生产服务器上的 web 应用程序的信息，请参阅 [调试已部署的 Web 应用程序](../debugger/debugging-deployed-web-applications.md)。  
  
 若要调试 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 应用程序，必须满足以下条件：  
  
- 您必须拥有必需的权限。 有关详细信息，请参阅 [System Requirements](../debugger/aspnet-debugging-system-requirements.md)。  
  
- [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 必须在 " **项目属性**" 中启用调试。  
  
- 一定要把你的应用程序配置文件 (Web.config) 设为调试模式。 调试模式会导致 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 为动态生成的文件生成符号，并允许将调试器附加到 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 应用程序。 如果项目是基于 Web 项目模板创建的，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 会在调试开始时自动完成这一设置。  
  
- 有关详细信息，请参阅 [如何：为 ASP.NET 应用程序启用调试](../debugger/how-to-enable-debugging-for-aspnet-applications.md)。  
  
### <a name="to-debug-a-web-application-during-development"></a>在开发过程中调试 Web 应用程序  
  
1. 在 " **调试** " 菜单上，单击 " **启动** " 以开始调试 Web 应用程序。  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 构建 Web 应用程序项目，根据需要部署应用程序，如果要在本地调试，则启动 ASP.NET 开发服务器，并附加到 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 工作进程。  
  
2. 使用调试器设置和清除断点，单步执行，并执行其他调试操作（就像调试任何应用程序那样）。  
  
     有关详细信息，请参阅 [调试器基础知识](../debugger/debugger-basics.md)。  
  
3. 在 " **调试** " 菜单上，单击 " **停止调试** " 以结束调试会话，或在 Internet Explorer 的 " **文件** " 菜单上，单击 " **关闭**"。  
  
## <a name="see-also"></a>另请参阅  
 [调试 Web 应用程序和脚本](../debugger/debugging-web-applications-and-script.md)   
 [调试 ASP.NET 和 AJAX 应用程序](../debugger/debugging-aspnet-and-ajax-applications.md)   
 [如何：为 ASP.NET 应用程序启用调试](../debugger/how-to-enable-debugging-for-aspnet-applications.md)
