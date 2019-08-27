---
title: Razor
description: 有关 Visual Studio for Mac 中 asp.net core 应用的 razor 支持的信息
author: sayedihashimi
ms.author: sayedha
ms.date: 05/03/2018
ms.topic: article
ms.technology: vs-ide-general
ms.assetid: F898CB6E-05ED-44CD-8DB6-427B2592CCC6
ms.openlocfilehash: 9e5a3f61ee7065a0615a381bdcc03dafc3566893
ms.sourcegitcommit: 7fbfb2a1d43ce72545096c635df2b04496b0be71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67691267"
---
# <a name="razor"></a>Razor

Visual Studio for Mac 提供对 Razor 编辑的支持，包括 .cshtml 文件中的 IntelliSense 和语法突出显示  。

![Visual Studio for Mac 中的 Razor 编辑](media/razor-editor.png)

本指南提供了创建第一个 Razor Web 应用的简介。 如需更详细的指南，请参阅 [.NET Core 文档中的 Razor Pages](/aspnet/core/razor-pages/index)。

## <a name="creating-a-new-razor-project"></a>创建新的 Razor 项目

* 在欢迎屏幕上，选择“新建”以创建新项目： 

![Visual Studio for Mac“新建项目”](media/razor-new.png)

* 在“新建项目”对话框中，导航到“.NET Core”   > “应用”   > “Web 应用程序”  ，然后选择“下一步”  按钮：

![Razor 项目模板](media/razor-new-project1.png)

* 选择所需的 .NET Core 目标框架（建议使用 2.2 或更高版本），然后选择“下一步”  。  为项目选择一个名称，并在需要时添加 git 支持。 选择“创建”  来创建项目。

![Razor 项目名称](media/razor-new-project2.png)

Visual Studio for Mac 将在代码布局中打开项目。

* 使用 Cmd-Opt-F5  运行该项目，无需调试。

Visual Studio 将启动 [Kestral](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel)，然后启动指向 `https://localhost:5001` 的浏览器并显示第一个 Razor Web 应用：

![Safari 中的 Razor Web 应用](media/razor-webapp.png)

## <a name="project-anatomy"></a>项目剖析

Razor Web 应用通常包含以下组件：

### <a name="pages-folder"></a>Pages 文件夹

可以在项目的 Pages 文件夹中找到网页，以及每个网页的代码隐藏：
* *.cshtml  文件对应 HTML 标记和 Razor 语法。
* *.cshtml.cs  文件对应用于处理页面事件的 C# 代码隐藏。

支持文件的名称以下划线开头。 例如，_Layout.cshtml 文件可配置所有页面通用的 UI 元素。 此文件设置页面顶部的导航菜单和页面底部的版权声明。 有关详细信息，请参阅 [ASP.NET Core 中的布局](https://docs.microsoft.com/aspnet/core/mvc/views/layout)。

### <a name="launch-settings"></a>启动设置

launchSettings.json  文件包含 IIS 设置、应用程序 URL 和其他相关设置。

### <a name="app-settings"></a>应用设置

appSettings,json  文件包含配置数据，如连接字符串。

有关配置的详细信息，请参阅 [ASP.NET 中的配置指南](https://docs.microsoft.com/aspnet/core/fundamentals/configuration/index)。

### <a name="wwwroot-folder"></a>wwwroot 文件夹

包含静态文件，如 HTML 文件、JavaScript 文件和 CSS 文件。 有关详细信息，请参阅 [ASP.NET Core 中的静态文件](https://docs.microsoft.com/aspnet/core/fundamentals/static-files)。

### <a name="programcs"></a>Program.cs

包含程序的入口点。 有关详细信息，请参阅 [ASP.NET Core Web 主机](https://docs.microsoft.com/aspnet/core/fundamentals/host/web-host)。

### <a name="startupcs"></a>Startup.cs

包含配置应用行为的代码，例如，是否需要同意 cookie。 有关详细信息，请参阅 [ASP.NET Core 中的应用启动](https://docs.microsoft.com/aspnet/core/fundamentals/startup)。

## <a name="see-aso"></a>另请参阅

有关创建 Razor Web 应用的更全面指南，请参阅 [ASP.NET Core 中的 Razor Pages 简介](https://docs.microsoft.com/aspnet/core/razor-pages/index)。
