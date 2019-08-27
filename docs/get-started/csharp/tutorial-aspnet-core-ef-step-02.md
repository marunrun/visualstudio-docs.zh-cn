---
title: 步骤 2：创建首个 ASP.NET Core Web 应用
description: 通过此视频教程和分步说明创建首个 ASP.NET Core Web 应用。
ms.custom: get-started
ms.date: 03/31/2019
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
monikerRange: vs-2019
ms.topic: tutorial
ms.devlang: CSharp
author: ardalis
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: 740d6336ab4258d3111dd6708de859108e22365e
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66402073"
---
# <a name="step-2-create-your-first-aspnet-core-web-app"></a>步骤 2：创建首个 ASP.NET Core Web 应用

通过此视频教程和分步说明创建首个 ASP.NET Core Web 应用。

观看此视频，按照说明创建首个 ASP.NET Core 应用。 

> [!VIDEO https://www.youtube.com/embed/-79RkpyFB6E]

## <a name="start-visual-studio-2019-and-create-a-new-project"></a>启动 Visual Studio 2019 并创建一个新项目

启动 Visual Studio 2019，然后单击“创建新项目”  。 选择“ASP.NET Core Web 应用程序”  。 选择“Web 应用程序”模板，并保留默认项目名和位置  。 单击 **“创建”** 。 有关更多详细说明，请参阅[本系列教程的上一个视频](tutorial-aspnet-core-ef-step-01.md)。

![Visual Studio 2019 选择 ASP.NET Core 项目选项](media/vs-2019/vs2019-choose-aspnetcore-project.png)

## <a name="explore-the-new-project"></a>浏览新项目

在右侧的“解决方案资源管理器”窗口中，可查看新项目的内容。 此处对其进行了介绍。

![Visual Studio 2019 ASP.NET Core 项目](media/vs-2019/vs2019-solution-explorer.png)

### <a name="wwwroot"></a>wwwroot

wwwroot 文件夹包含可从 Web 应用程序公开访问的静态文件  。 它通常包含样式表、客户端脚本文件和图像。

### <a name="pages"></a>Pages

Pages 文件夹包含站点的 Razor Pages  。 默认模板提供了多个页面，其中包括应用程序主页 Index.cshtml 页面，以及“关于”、“联系人”等  。

### <a name="appsettingsjson"></a>appsettings.json

此文件包含站点的配置设置（JSON 格式）。

### <a name="programcs"></a>Program.cs

此文件充当应用程序的入口点。 当应用运行时，其 Main 方法是运行的第一个方法，负责创建包含应用程序的 Web 主机。

### <a name="startupcs"></a>Startup.cs

在 Program.cs 中创建的 Web 主机引用 Startup 类并调用其方法来配置应用程序  。 ConfigureServices 方法负责设置应用使用的任何服务。 `Configure` 方法设置应用的 HTTP 请求管道。 每个请求都会通过此管道，并在此过程中与每个中间件进行交互  。

### <a name="indexcshtml"></a>Index.cshtml

站点的主页包含一些 HTML 标记和一些服务器端 Razor 代码。 它使用 Razor 来指定位于相关 Index.cshtml.cs 文件中的页面模型 `IndexModel`  。 它还通过设置 ViewData 中的值设置了页标题。 此 ViewData 值在 \_Layout.cshtml 文件中读取，该文件位于 Shared 文件夹中的 Pages 文件夹内  。 Layout 文件由许多 Razor Pages 共享，并为应用程序提供通用外观。 每个页面的内容都在 Layout 文件的 HTML 中呈现。

## <a name="run-the-application"></a>运行此应用程序

现在运行应用程序，并在浏览器中查看。 可通过使用 Ctrl+F5 或通过从 Visual Studio 的菜单中选择“调试” > “开始执行(不调试)”来运行应用程序     。

## <a name="customize-the-application"></a>自定义应用程序

将属性添加到 Index.cshtml.cs文件，并将其值设置为 `OnGet` 处理程序中的当前时间  ：

```csharp
public string Time { get; set; }
public void OnGet()
{
    Time = DateTime.Today.ToShortTimeString();
}
```

将 Index.cshtml 中的 `<div>` 内容替换为以下标记  ：

```cshtml
<h2>It's @Model.Time right now on the server!</h2>
```

再次运行该应用程序。 你可看到此页面现在显示当前时间，但始终是午夜！ 这不正确。

![Visual Studio 2019 浏览器中的 ASP.NET Core 项目](media/vs-2019/vs2019-app-in-browser.png)

## <a name="debug-the-application"></a>调试应用程序

向 `OnGet` 方法添加一个断点，向其中的 `Time` 赋值，并在此次开始执行时调试应用程序。

执行过程在包含该断点的行处停止，可看到 `DateTime.Today` 包括日期，但时间始终是午夜，因为它不包括时间数据。 

![Visual Studio 2019 浏览器中的 ASP.NET Core 项目](media/vs-2019/vs2019-breakpoint.png)

将其更改为使用 `DateTime.Now` 并继续执行。 `OnGet` 的新代码应为：

```csharp
public void OnGet()
{
    Time = DateTime.Now.ToShortTimeString();
}
```

现在导航到应用时，可在浏览器中看到实际的服务器时间。

> [!NOTE]
> 输出可能与映像不同，因为 ToShortDateTimeString 的输出格式取决于当前区域性设置。 请参阅 <xref:System.DateTime.ToShortTimeString>。

![Visual Studio 2019 浏览器中的 ASP.NET Core 项目](media/vs-2019/vs2019-app-fixed-in-browser.png)

## <a name="next-steps"></a>后续步骤

下一个视频介绍了如何将数据支持添加到应用。

[教程：在 ASP.NET Core 应用中处理数据](tutorial-aspnet-core-ef-step-03.md)

## <a name="see-also"></a>请参阅

- [教程：使用 ASP.NET Core 创建 Razor Pages Web 应用](/aspnet/core/tutorials/razor-pages/?view=aspnetcore-2.1)
