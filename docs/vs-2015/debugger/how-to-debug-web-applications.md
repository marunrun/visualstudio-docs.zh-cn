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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205402"
---
# <a name="how-to-debug-web-applications"></a>如何：调试 Web 应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 是用于开发 Web 应用程序中的主要技术[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 调试器为在本地或远程服务器上调试 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web 应用程序提供了强大的工具。 本主题介绍如何调试[!INCLUDE[vstecasp](../includes/vstecasp-md.md)]在开发过程中的项目。 有关如何调试信息[!INCLUDE[vstecasp](../includes/vstecasp-md.md)]Web 应用程序已部署在生产服务器上，请参阅[调试部署 Web 应用程序](../debugger/debugging-deployed-web-applications.md)。  
  
 若要调试 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 应用程序，必须满足以下条件：  
  
- 您必须拥有必需的权限。 有关详细信息，请参阅 [System Requirements](../debugger/aspnet-debugging-system-requirements.md)。  
  
- [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 必须在启用调试**项目属性**。  
  
- 一定要把你的应用程序配置文件 (Web.config) 设为调试模式。 调试模式会导致 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 为动态生成的文件生成符号，并允许将调试器附加到 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 应用程序。 如果项目是基于 Web 项目模板创建的，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 会在调试开始时自动完成这一设置。  
  
- 有关详细信息，请参阅[如何：为 ASP.NET 应用程序启用调试](../debugger/how-to-enable-debugging-for-aspnet-applications.md)。  
  
### <a name="to-debug-a-web-application-during-development"></a>在开发过程中调试 Web 应用程序  
  
1. 上**调试**菜单上，单击**启动**开始调试 Web 应用程序。  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 将生成 Web 应用程序项目，根据需要部署应用程序，启动 ASP.NET Development Server（如果正在进行本地调试），并附加到 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 辅助进程。  
  
2. 使用调试器设置和清除断点，单步执行，并执行其他调试操作（就像调试任何应用程序那样）。  
  
     有关详细信息，请参阅[调试器基础知识](../debugger/debugger-basics.md)。  
  
3. 上**调试**菜单上，单击**停止调试**结束调试会话，或在**文件**菜单中 Internet Explorer 中，单击**关闭**。  
  
## <a name="see-also"></a>请参阅  
 [Debugging Web Applications and Script](../debugger/debugging-web-applications-and-script.md) （调试 Web 应用程序和脚本）  
 [调试 ASP.NET 和 AJAX 应用程序](../debugger/debugging-aspnet-and-ajax-applications.md)   
 [如何：为 ASP.NET 应用程序启用调试](../debugger/how-to-enable-debugging-for-aspnet-applications.md)
