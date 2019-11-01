---
title: 查找正在运行的 ASP.NET 进程 |Microsoft Docs
ms.date: 11/04/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- ASP.NET debugging, ASP.NET process
- ASP.NET process
ms.assetid: 931a7597-b0f0-4a28-931d-46e63344435f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: 54aa98dd238d7a78e4ae89af05dceae0f9911478
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73187655"
---
# <a name="find-the-name-of-the-aspnet-process"></a>查找 ASP.NET 进程的名称

若要调试正在运行的 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 应用程序，Visual Studio 调试器必须按名称附加到 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 进程。

**确定哪个进程正在运行 ASP.NET 应用程序：**

1. 应用运行时，在 Visual Studio 中选择 "**调试**" > "**附加到进程**"。

1. 在 "**附加到进程**" 对话框中，键入以下列表中的第一个字母，或在 "搜索" 框中输入这些名称。 正在运行的应用程序是运行 ASP.NET 应用程序的应用程序。 附加到该进程以调试应用程序。

    - *w3wp.exe*是 IIS 6.0 及更高版本。
    - *aspnet_wp.exe*是早期版本的 IIS。
    - *iisexpress*为 iisexpress。
    - *dotnet* ASP.NET Core。
    - *inetinfo*是在进程内运行的较旧的 ASP 应用程序。

>[!NOTE]
>Visual Studio 2012 及更早版本的 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 代码可以位于文件系统上，并在测试服务器*webdev.webserver.exe*或*webdev.webserver.exe*上运行。 在这种情况下，对于本地调试，附加到*webdev.webserver.exe*或*webdev.webserver.exe* ，而不是 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 进程。

**另请参阅：**

- [附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [远程调试 web 应用程序的先决条件](remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)
- [系统要求](../debugger/aspnet-debugging-system-requirements.md)
- [调试 ASP.NET 应用程序](../debugger/how-to-enable-debugging-for-aspnet-applications.md)