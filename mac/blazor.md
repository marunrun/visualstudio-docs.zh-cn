---
title: 创建 Blazor Web 应用
description: 提供了有关 Visual Studio for Mac 中 ASP.NET Core 应用的 Blazor 支持的信息。
author: jongalloway
ms.author: jogallow
ms.date: 12/17/2019
ms.technology: vs-ide-general
ms.assetid: D2717D3A-9225-40A8-8155-7D0143B2CA60
ms.openlocfilehash: dbc49a0ea9b4e4fa7880b6226331d447339b6575
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "75737299"
---
# <a name="create-blazor-web-apps"></a>创建 Blazor Web 应用

本指南介绍如何创建第一个 Blazor Web 应用。 若需要更深入的指导，请参阅 [ASP.NET Core Blazor 简介](/aspnet/core/blazor/index)。

Visual Studio for Mac（从版本 8.4 开始）支持开发和发布 ASP.NET Core Blazor Server 应用程序。 Blazor 是一个框架，用于通过 .NET 构建交互式客户端 Web UI，进而为 Web 开发人员提供以下优势：

* 使用 C# 代替 JavaScript 来编写代码。
* 利用现有的 .NET 库生态系统。
* 在服务器和客户端之间共享应用逻辑。
* 受益于 .NET 的性能、可靠性和安全性。
* 始终高效支持电脑、Linux 和 macOS 上的 Visual Studio。
* 以一组稳定、功能丰富且易用的通用语言、框架和工具为基础来进行生成。

## <a name="creating-a-new-blazor-project"></a>创建新的 Blazor 项目

1. 在“开始”  窗口上，选择“新建”  创建新项目：

   ![突出显示“新建”选项的 Visual Studio for Mac“开始”窗口](media/blazor-new-project.png)
1. 在“新建项目”  对话框中，选择“.NET Core”  >“应用”  >“Blazor Server 应用”  ，然后选择“下一步”  ：![为“新建项目”对话框选择一个模板，并选择“Blazor Server 应用”模板](media/blazor-project-template.png)

1. 选择 .NET Core 3.1 作为目标框架，然后选择“下一步”  。 
   ![配置新的 Blazor Server 应用对话框，其中显示了选择到 .NET Core 3.1 的目标框架](media/blazor-select-target-framework.png)

1. 为项目选择一个名称，并在需要时添加 Git 支持。 选择“创建”  创建项目。
   ![配置在输入项目名称时显示的新 Blazor Server 应用对话框](media/blazor-name-project.png)

   Visual Studio for Mac 会在代码布局窗口中打开项目。
1. 选择“运行”   > “开始执行(不调试)”  以运行应用。

   Visual Studio 将启动 [Kestral](/aspnet/core/fundamentals/servers/kestrel)，然后打开浏览器转至 `https://localhost:5001` 并显示 Blazor Web 应用。

   ![Safari 中的 Blazor Web 应用](media/blazor-new-app-in-edge.png)

## <a name="blazor-support-in-visual-studio-for-mac"></a>Visual Studio for Mac 中的 Blazor 支持

Visual Studio for Mac（从版本 8.4 开始）包含新功能，可帮助你创建新的 Blazor Server 项目。 此外，它还提供所需的标准支持，如生成、运行和调试 Blazor 项目。 

在上面的演练中，我们看到了 Blazor Server 应用项目模板如何帮助你创建新的 Blazor Server 应用项目。 让我们看看 Visual Studio for Mac 中的一些附加功能，以支持 Blazor 服务器项目开发。

### <a name="editor-support-for-razor-files"></a>编辑器支持 .razor  文件
Visual Studio for Mac 支持编辑 .razor 文件 - 创建 Blazor 应用程序时将使用的大多数文件。 Windows 和 Mac 版本的 IDE 对 razor 文件共享相同的编辑器。 你将看到对 .razor 文件的完整着色和完成支持，包括项目中声明的 Razor 组件的完成情况。

![显示 Blazor Intellisense 的 Visual Studio for Mac 编辑器窗口](media/blazor-intellisense.png)

### <a name="publishing-blazor-applications-to-azure-app-service"></a>将 Blazor 应用程序发布到 Azure 应用服务
你还可以将 Blazor 应用程序直接发布到 Azure 应用服务。 如果没有用于在 Azure 上运行 Blazor 应用的 Azure 帐户，你始终可以[在此处注册一个免费帐户](https://azure.microsoft.com/free)，可享受 12 个月的免费热门服务，200 美元的免费 Azure 额度，以及超过 25 项永久免费服务。

![显示 Azure 发布体验的 Visual Studio for Mac](media/blazor-azure-publish.png)

## <a name="project-anatomy"></a>项目剖析

默认情况下，Blazor Web 应用包含几个目录和文件。 在开始时，你需要熟悉以下主要内容：

### <a name="pages-folder"></a>Pages 文件夹

此文件夹包含项目网页，网页使用 .razor  文件扩展名。

### <a name="shared-folder"></a>Shared 文件夹

此文件夹包括共享组件，同样使用 .razor  扩展名。 你将看到其中包括 MainLayout.razor  ，用于定义应用程序中的通用布局。 它还包括在所有页面上使用的共享 NavMenu.razor  组件。 如果要创建可重用的组件，它们将置于 Shared  文件夹中。

### <a name="app-settings"></a>应用设置

appSettings,json 文件包含配置数据，如连接字符串  。

有关配置的详细信息，请参阅 [ASP.NET 中的配置指南](/aspnet/core/fundamentals/configuration/index)。

### <a name="wwwroot-folder"></a>wwwroot 文件夹

此文件夹包含静态文件，如 HTML、JavaScript 和 CSS 文件。 有关详细信息，请参阅 [ASP.NET Core 中的静态文件](/aspnet/core/fundamentals/static-files)。

### <a name="programcs"></a>Program.cs

此文件包含程序的入口点。 有关详细信息，请参阅 [ASP.NET Core Web 主机](/aspnet/core/fundamentals/host/web-host)。

### <a name="startupcs"></a>Startup.cs

此文件包含配置应用行为的代码，例如该应用是否需要 cookie 的同意。 有关详细信息，请参阅 [ASP.NET Core 中的应用启动](/aspnet/core/fundamentals/startup)。

## <a name="summary"></a>总结
在本教程中，你已了解如何在 Visual Studio for Mac 中创建新的 Blazor Server 应用，并了解了一些 Visual Studio for Mac 提供的可帮助你创建 Blazor 应用程序的功能。

## <a name="see-also"></a>请参阅

有关创建 Blazor Web 应用的更全面指南，请参阅 [ASP.NET Core Blazor 简介](/aspnet/core/blazor/index)。
