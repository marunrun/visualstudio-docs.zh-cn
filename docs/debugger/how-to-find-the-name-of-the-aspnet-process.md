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
ms.openlocfilehash: 27221a4ae47b9fb06130b550ceb6d3cc1f00dce0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62906799"
---
# <a name="find-the-name-of-the-aspnet-process"></a>查找 ASP.NET 进程的名称

若要调试正在运行[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]应用程序中，Visual Studio 调试器必须附加到[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]进程的名称。

**若要查看哪个进程正在运行的 ASP.NET 应用：**

1. 与应用程序运行，请在 Visual Studio 中，选择**调试** > **附加到进程**。

1. 在中**附加到进程**对话框中，键入过程的第一个字母从以下列表中，名称或搜索框中输入它们。 一个正在运行的是运行 ASP.NET 应用程序。 附加到该进程来调试应用程序。

    - *w3wp.exe*是 IIS 6.0 及更高版本。
    - *aspnet_wp.exe*是 IIS 的早期版本。
    - *iisexpress.exe*是 IISExpress。
    - *dotnet.exe*是 ASP.NET Core。
    - *inetinfo.exe*是在进程中运行的旧版 ASP 应用程序。

>[!NOTE]
>Visual Studio 2012 及更早[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]位于文件系统上并在测试服务器上运行代码*WebDev.WebServer.exe*或*WebDev.WebServer40.exe*。 在这种情况下，对于本地调试，附加到*WebDev.WebServer.exe*或*WebDev.WebServer40.exe*而不是[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]过程。

**另请参阅：**

- [附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [远程调试 web 应用程序的先决条件](/visualstudio/debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer)
- [系统要求](../debugger/aspnet-debugging-system-requirements.md)
- [调试 ASP.NET 应用程序](../debugger/how-to-enable-debugging-for-aspnet-applications.md)