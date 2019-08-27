---
title: 远程调试 Web 应用程序的必备组件 |Microsoft Docs
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
- debugging ASP.NET Web applications, remote servers
- remote debugging, prerequisites
- remote servers, debugging Web applications
ms.assetid: 1cd777b5-6d20-4ca6-a0df-51653b118469
caps.latest.revision: 30
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c13cfdeb90fae554479c7dc8a68261f40bc4cfc6
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65690112"
---
# <a name="prerequistes-for-remote-debugging-web-applications"></a>远程调试 Web 应用程序的必备组件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 调试器，你可以在本地计算机或远程服务器上以透明方式调试 Web 应用程序。 这意味着，调试器始终以相同的方式运行，因而允许您在任一计算机上使用相同的功能。 但若要使远程调试正常进行，有一些先决条件。  
  
- 必须在要调试的服务器上安装 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 远程调试组件。 有关详细信息，请参阅[设置远程调试](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)。  
  
- 默认情况下，[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 辅助进程作为 ASPNET 用户进程运行。 因此，您必须在运行 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 的计算机上拥有管理员特权，才能对其进行调试。 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 辅助进程的名称因调试方案和 IIS 版本而异。 有关详细信息，请参阅[如何：查找 ASP.NET 进程名称](../debugger/how-to-find-the-name-of-the-aspnet-process.md)。  
  
## <a name="see-also"></a>请参阅  
 [调试 ASP.NET 和 AJAX 应用程序](../debugger/debugging-aspnet-and-ajax-applications.md)   
 [系统要求](../debugger/aspnet-debugging-system-requirements.md)
