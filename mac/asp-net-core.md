---
title: ASP.NET Core 入门
description: 本文介绍如何在 Visual Studio for Mac 中开始使用 ASP.NET，包括安装和创建新项目。
author: sayedihashimi
ms.author: sayedha
ms.date: 04/02/2019
ms.assetid: 6E8B0C90-33D6-4546-8207-CE0787584565
ms.custom: video
no-loc:
- Blazor
- Blazor WebAssembly
ms.topic: how-to
ms.openlocfilehash: ed92205388202c457f4d6c8e3fbba567a0d5944e
ms.sourcegitcommit: 5e82a428795749c594f71300ab03a935dc1d523b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2020
ms.locfileid: "86211654"
---
# <a name="getting-started-with-aspnet-core"></a>ASP.NET Core 入门

 Visual Studio for Mac 支持最新的 ASP.NET Core Web 开发平台，使你可轻松开发自己的应用服务。 ASP.NET Core 运行于 .NET Core 上，后者是 .NET Framework 和运行时的最新发展。 它经过调优，可提供极快的性能，进行分解后，更便于小规模安装，且经过重新构思设计，可在 Linux 和 macOS 以及 Windows 上运行。

## <a name="installing-net-core"></a>安装 .NET Core

安装 Visual Studio for Mac 时，将自动安装 .NET Core 3.1。 有关 Visual Studio for Mac 中支持的 .NET Core 版本的详细信息，请参阅 [.NET Core 支持](/visualstudio/mac/net-core-support)。

## <a name="creating-an-aspnet-core-app-in-visual-studio-for-mac"></a>在 Visual Studio for Mac 中创建 ASP.NET Core 应用

打开 Visual Studio for Mac。 在开始屏幕上，选择“新建项目…”

![“新建项目”对话框](media/asp-net-core-2019-new-asp-core.png)

这将显示“新建项目”对话框，可通过它选择模板创建应用程序。

许多项目都提供有预建模板，方便快速开始创建 ASP.NET Core 应用程序。 这些是：

- **.NET Core > 空**
- **.NET Core > API**
- **.NET Core > Web 应用**
- **.NET Core > Web 应用（模型-视图-控制器）**
- **.NET Core > Blazor Server 应用**
- **.NET Core > Blazor WebAssembly 应用**

![ASP.NET 项目选项](media/asp-net-core-2019-new-asp-core.png)

选择“ASP.NET Core 空 Web 应用”，然后按“下一步” 。 为项目指定名称，并按“创建”。 这会创建新的 ASP.NET Core 应用。 在 Solution Pad 的左窗格中，展开第二个箭头，然后选择“Startup.cs”。 如下图所示：

![新 ASP.NET Core 空项目视图](media/asp-net-core-2019-empty-project.png)

ASP.NET Core 空模板通过以下两个默认文件创建一个 Web 应用程序：Program.cs 和 Startup.cs，后面将对这两个文件进行说明。 它还将创建一个依赖项文件夹，该文件夹包含项目的 NuGet 包依赖项，如 ASP.NET Core、.NET Core 框架和生成该项目的 MSBuild 目标：

![显示依赖项的 Solution Pad](media/asp-net-core-2019-solution-dependencies.png)

### <a name="programcs"></a>Program.cs

在项目中打开并检查“Program.cs”文件。 请注意，在 `Main` 方法中会发生几件事 – 应用中的项：

```csharp
    public class Program
    {
        public static void Main(string[] args)
        {
            CreateWebHostBuilder(args).Build().Run();
        }

        public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
            WebHost.CreateDefaultBuilder(args)
                .UseStartup<Startup>();
    }
```

ASP.NET Core 应用将通过 [`WebHostBuilder`](/aspnet/core/fundamentals/hosting) 实例配置并启动主机，以此在其 Main 方法中创建一个 Web 服务器。 此生成器提供方法以允许配置主机。 在模板应用中使用了以下配置：

* `.UseStartup<Startup>()`：指定启动类。

但是，也可以添加其他配置，例如：

* `UseKestrel`：指定应用将使用的 Kestrel 服务器
* `UseContentRoot(Directory.GetCurrentDirectory())`：从 Web 项目的根文件夹启动应用时，使用此文件夹作为应用的内容根
* `.UseIISIntegration()`：指定应用应使用 IIS。 要在 ASP.NET Core 中使用 IIS，需要指定 `UseKestrel` 和 `UseIISIntegration`。

### <a name="startupcs"></a>Startup.cs

可在 `CreateWebHostBuilder` 上的 `UseStartup()` 方法中指定应用的 Startup 类。 在此类中，可指定请求处理管道和配置任何服务。

在项目中打开并检查“Startup.cs”文件：

```csharp
    public class Startup
    {
        // This method gets called by the runtime. Use this method to add services to the container.
        // For more information on how to configure your application, visit https://go.microsoft.com/fwlink/?LinkID=398940
        public void ConfigureServices(IServiceCollection services)
        {
        }

        // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
        public void Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }

            app.Run(async (context) =>
            {
                await context.Response.WriteAsync("Hello World!");
            });
        }
    }
```

Startup 类必须始终遵守以下规则：

- 始终为公共
- 包含两个公共方法：`ConfigureServices` 和 `Configure`

`ConfigureServices` 方法定义将在应用中使用的服务。

通过 `Configure` 可使用 [Middleware](/aspnet/core/fundamentals/middleware) 撰写请求管道。 将在 ASP.NET 应用程序管道中使用这些组件，用于处理请求和响应。 HTTP 管道包含大量按顺序调用的请求委托。 每个委托可选择处理请求本身，或将其传递给下一个委托。

可通过在 `IApplicationBuilder` 上使用 `Run`、`Map` 和 `Use` 方法配置委托。但 `Run` 方法不会调用下一个委托，应始终用于管道末尾。

预建模板的 `Configure` 方法有数种作用。 首先，它会配置开发中使用的意外处理页面。 其次，它会向请求网页发送响应，内容为简单的“Hello World”。

不添加任何其他代码也可运行此简单的“Hello, World”项目。 若要运行应用，可以使用“播放”按钮的下拉列表选择要在其中运行应用的浏览器，或只需点击“播放”（三角形）按钮即可使用默认浏览器：

![浏览器运行](media/asp-net-web-picker.png)

Visual Studio for Mac 使用随机端口启动 Web 项目。 要找到该端口，请打开“视图”>“面板”下列出的“应用程序输出”。 之后应找到类似下图内容的输出：

![显示侦听端口的应用程序输出](media/asp-net-core-image6.png)

项目运行后，默认 web 浏览器应启动并连接到“应用程序输出”中列出的 URL。 或者，可以打开选择的任何浏览器，输入 `http://localhost:5000/`，将 `5000` 替换为“应用程序输出”中 Visual Studio 输出的端口。 将显示文本 `Hello World!`：

![显示文本的浏览器](media/asp-net-core-image7.png)

## <a name="adding-a-controller"></a>添加控制器

ASP.NET Core 应用使用模型视图控制器 (MVC) 设计模式，来为应用的每一部分提供职责逻辑分离。 MVC 包括以下几个部分：

- **模型**：代表应用数据的类。
- **视图**：显示应用的用户界面（通常为模型数据）。
- **控制器**：处理浏览器请求的类，响应用户的输入和交互。

有关使用 MVC 的详细信息，请参阅 [Overview of ASP.NET Core MVC](/aspnet/core/mvc/overview)（ASP.NET Core MVC 概述）。

要添加控制器，请执行下列操作：

1. 右键单击项目名称，然后选择“添加”>“新文件”。 选择“常规”>“空类”，然后输入控制器名称：

    ![“新文件”对话框](media/asp-net-core-image8.png)

2. 向新控制器添加以下代码：

    ```csharp
    using System;
    using Microsoft.AspNetCore.Mvc;
    using System.Text.Encodings.Web;

    namespace Hello_ASP
    {
        public class HelloWorldController : Controller
        {
            //
            // GET: /HelloWorld/

            public string Index()
            {
                return "This is my default action...";
            }

        }
    }
    ```

3. 通过右键单击“依赖项”文件夹并选择“添加包...”来添加 `Microsoft.AspNetCore.Mvc` 依赖项 。

4. 使用搜索框浏览 NuGet 库，查找其中的 `Microsoft.AspNetCore.Mvc`，然后选择“添加包”。 安装可能需要几分钟时间，系统将提示你为必需的依赖项接受各种许可证：

    ![添加 NuGet](media/asp-net-core-image9.png)

5. 在 Startup 类中，删除 `app.Run` lambda并设置 URL 路由逻辑，MVC 将用其决定应调用到以下内容的代码：

    ```csharp
    app.UseMvc(routes =>
    {
        routes.MapRoute(
        name: "default",
        template: "{controller=HelloWorld}/{action=Index}/{id?}");
    });
    ```

    请务必删除 `app.Run` lambda，因为这将重写路由逻辑。

    MVC 使用以下格式来决定运行的代码：

    `/[Controller]/[ActionName]/[Parameters]`

    添加以上代码片段相当于告诉应用默认为 `HelloWorld` 控制器和 `Index` 操作方法。

6. 将 `services.AddMvc();` 调用添加到 `ConfigureServices` 方法，如下图所示：

    ```csharp
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddMvc();
    }
    ```

    也可将参数信息从 URL 传递到控制器。

7. 向 HelloWorld 控制器添加另一方法，如下图所示：

    ```csharp
    public string Xamarin(string name)
    {
        return HtmlEncoder.Default.Encode($"Hello {name}, welcome to Visual Studio for Mac");
    }
    ```

8. 如果现在运行应用，它应自动打开浏览器：

    ![在浏览器中运行应用](media/asp-net-core-image13.png)

9. 尝试浏览到 `http://localhost:xxxx/HelloWorld/Xamarin?name=Amy`（使用正确端口替代 `xxxx`），应显示如下信息：

    ![通过参数在浏览器中运行应用](media/asp-net-core-image10.png)

## <a name="troubleshooting"></a>疑难解答

若需要在 Mac OS 10.12 (Sierra) 或更高版本上手动安装 .NET Core，请执行以下操作：

1. 安装 .NET Core 前，请确保所有 OS 更新已更新至最新的稳定版本。 可转到应用商店应用程序，并选择“更新”选项卡对此进行检查。

2. 请遵循 [.NET Core 站点](https://www.microsoft.com/net/core#macos) 上列出的步骤。

请确保成功完成所有步骤，以确保成功安装 .NET Core。

## <a name="summary"></a>总结

本指南介绍了 ASP.NET Core。 介绍了它是什么，何时使用，并提供了在 Visual Studio for Mac 中使用它的信息。
有关后续步骤的详细信息，请参阅以下指南：
- [ASP.NET Core ](/aspnet/core/?view=aspnetcore-2.1) 文档。
- [Creating Backend Services for Native Mobile Applications（为本地移动应用程序创建后端服务）](/aspnet/core/mobile/native-mobile-backend)，介绍了如何使用 ASP.NET Core 为 Xamarin.Forms 应用生成 REST 服务。
- [ASP.NET Core 动手实验](https://github.com/Microsoft/vs4mac-labs/tree/master/Web/Getting-Started)。

## <a name="related-video"></a>相关视频

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Build-Your-First-App/player]
