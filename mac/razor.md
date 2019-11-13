---
title: 创建 Razor Web 应用
description: 提供有关 Visual Studio for Mac 中 ASP.NET Core 应用的 Razor 支持的信息。
author: sayedihashimi
ms.author: sayedha
ms.date: 05/03/2018
ms.technology: vs-ide-general
ms.assetid: F898CB6E-05ED-44CD-8DB6-427B2592CCC6
ms.openlocfilehash: fe9ef921ccfc42b77bd08925805aeac6f4aec777
ms.sourcegitcommit: ba0fef4f5dca576104db9a5b702670a54a0fcced
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73715877"
---
# <a name="create-razor-web-apps"></a>创建 Razor Web 应用

本指南介绍如何创建第一个 Razor Web 应用。 若需要更深入的指导，请参阅 [ASP.NET Core 中的 Razor Pages 介绍](/aspnet/core/razor-pages/index)。

Visual Studio for Mac 提供对 Razor 编辑的支持，包括 .cshtml 文件中的 IntelliSense 和语法突出显示  。 Visual Studio 2019 for Mac 8.3+ 中的新增功能可在 Razor 文件中拥有上下文感知 IntelliSense，从而能接收与当前在文档中编辑的语言相匹配的 IntelliSense。

![Visual Studio for Mac 中的 Razor 编辑](media/razor-2019.png)

## <a name="creating-a-new-razor-project"></a>创建新的 Razor 项目

1. 在欢迎屏幕上，选择“新建”以创建新项目  ：

   ![Visual Studio for Mac“新建项目”](media/razor-new.png)
1. 在“新建项目”对话框中，转到“.NET Core” > “应用” > “Web 应用程序”，然后选择“下一步”      ：

   ![Razor 项目模板](media/razor-new-project1.png)
1. 选择你的 .NET Core 目标框架（建议使用 2.2 或更高版本），然后选择“下一步”  。 为项目选择一个名称，并在必要时添加 Git 支持。 选择“创建”  来创建项目。

   ![Razor 项目名称](media/razor-new-project2.png)

   Visual Studio for Mac 会在代码布局窗口中打开项目。
1. 使用 Command+Option+F5 运行该项目，无需调试  。

   Visual Studio 将启动 [Kestral](/aspnet/core/fundamentals/servers/kestrel)，然后打开浏览器转至 `https://localhost:5001` 并显示第一个 Razor Web 应用。

   ![Safari 中的 Razor Web 应用](media/razor-webapp.png)

## <a name="project-anatomy"></a>项目剖析

Razor Web 应用包含以下组件。

### <a name="pages-folder"></a>Pages 文件夹

此文件夹包含项目的网页，以及每个网页的代码隐藏：
   - \*.cshtml 文件对应 HTML 标记和 Razor 语法  。
   - \*.cshtml.cs  文件对应用于处理页面事件的 C# 代码隐藏。

支持文件的名称以下划线开头。 例如，_Layout.cshtml 文件可配置所有页面通用的 UI 元素。 此文件设置页面顶部的导航菜单和页面底部的版权声明。 有关详细信息，请参阅 [ASP.NET Core 中的布局](/aspnet/core/mvc/views/layout)。

### <a name="launch-settings"></a>启动设置

launchSettings.json 文件包含 IIS 设置、应用程序 URL 和其他相关设置  。

### <a name="app-settings"></a>应用设置

appSettings,json 文件包含配置数据，如连接字符串  。

有关配置的详细信息，请参阅 [ASP.NET 中的配置指南](/aspnet/core/fundamentals/configuration/index)。

### <a name="wwwroot-folder"></a>wwwroot 文件夹

此文件夹包含静态文件，如 HTML、JavaScript 和 CSS 文件。 有关详细信息，请参阅 [ASP.NET Core 中的静态文件](/aspnet/core/fundamentals/static-files)。

### <a name="programcs"></a>Program.cs

此文件包含程序的入口点。 有关详细信息，请参阅 [ASP.NET Core Web 主机](/aspnet/core/fundamentals/host/web-host)。

### <a name="startupcs"></a>Startup.cs

此文件包含配置应用行为的代码，例如该应用是否需要 cookie 的同意。 有关详细信息，请参阅 [ASP.NET Core 中的应用启动](/aspnet/core/fundamentals/startup)。

## <a name="see-also"></a>请参阅

有关创建 Razor Web 应用的更全面指南，请参阅 [ASP.NET Core 中的 Razor Pages 简介](/aspnet/core/razor-pages/index)。
