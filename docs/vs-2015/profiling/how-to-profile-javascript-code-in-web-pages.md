---
title: 如何：分析网页中的 JavaScript 代码 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- JavaScript performance profiling
- Profiling Tools,JavaScript
- web site performance profiling
ms.assetid: 37d02aad-ca4d-4eb0-bf66-ca3ecef31fbe
caps.latest.revision: 32
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: aa504e961ed8e592f5e3df84ff7a688fa2398200
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65688149"
---
# <a name="how-to-profile-javascript-code-in-web-pages"></a>如何：分析网页中的 JavaScript 代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 分析工具可以通过使用检测分析方法收集在 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web 应用程序、任意网页或 JavaScript 应用程序中执行的 JavaScript 代码的性能数据。  
  
 **要求**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
- Internet Explorer 8 或更高版本。  
  
> [!WARNING]
> 若要分析 Windows 应用商店应用中的 JavaScript，请参阅以下主题之一：  
> 
> - [Javascript 函数计时](https://msdn.microsoft.com/library/b2bf49fc-aea7-4d9c-8fcf-cff8b8dd0c03) [Javascript 函数在远程设备上计时](https://msdn.microsoft.com/library/d78812b6-a97e-46dc-8d99-e724d1d725d8)  
>   - [分析 JavaScript 函数的计时数据](https://msdn.microsoft.com/library/b5aea8d8-36df-47ba-a7ca-95406700ca9b)  
>   - 
  
 可以使用“分析向导”创建性能会话。 指定检测方法，然后在该性能会话的属性对话框的“检测”页上指定 JavaScript 分析选项。  
  
 如果指定 JavaScript 分析，则将同时分析在浏览器中执行的 JavaScript 代码以及在服务器中执行的 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 代码。  
  
- 对于 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web 应用程序，将同时分析在浏览器中执行的 JavaScript 代码以及在服务器中执行的 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 代码。  
  
- 对于任意网页，将分析在浏览器中执行的 JavaScript 代码。  
  
### <a name="to-profile-javascript-in-an-aspnet-web-application-project"></a>分析 ASP.NET Web 应用程序项目中的 JavaScript  
  
1. 在 [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]中，打开 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web 项目。  
  
2. 在“分析”  菜单上，单击“启动性能向导” 。  
  
3. 在“性能向导”的第一页上，指定“检测”  分析方法，然后单击“下一步” 。  
  
4. 在向导的第二页上，确保在目标列表中选择了当前项目，然后单击“下一步”   
  
5. 在向导的第三页上，选中“分析 JavaScript”  复选框，然后单击“下一步” 。  
  
6. 在向导的第四页上，单击 " **完成** "，在浏览器中启动 Web 应用程序。  
  
7. 练习要分析的功能。  
  
8. 若要结束分析会话，请关闭浏览器。  
  
### <a name="to-profile-javascript-in-individual-web-pages-or-a-javascript-applications"></a>分析各网页或 JavaScript 应用程序中的 JavaScript  
  
1. 打开 [!INCLUDE[vsPreShort](../includes/vspreshort-md.md)]。  
  
2. 在“分析”  菜单上，单击“启动性能向导” 。  
  
3. 在“性能向导”的第一页上，指定“检测”  分析方法，然后单击“下一步” 。  
  
4. 在向导的第二页上，单击 ASP.NET 或 JavaScript 应用程序，然后单击“下一步”   
  
5. 在向导的第三页上：  
  
    1. 在“将运行应用程序的 URL 或路径”  框中键入网页的 URL。  
  
    2. 选中“分析 JavaScript”  复选框，然后单击“下一步” 。  
  
6. 在向导的第四页上，单击 " **完成** "，在浏览器中启动网页。  
  
7. 练习要分析的功能。  
  
8. 若要结束分析会话，请关闭浏览器。
