---
title: 生成 ASP.NET Core 应用程序
description: 本文介绍如何在 Visual Studio for Mac 中开始使用 ASP.NET，包括安装和创建新项目。
author: sayedihashimi
ms.author: sayedha
ms.date: 05/30/2019
ms.assetid: 771C2F8E-46BC-4280-AFE8-ED9D5C7790CE
ms.openlocfilehash: 345111144e0e209d91d34e53fefcd7d1207d9a8a
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68872468"
---
# <a name="building-aspnet-core-applications-in-visual-studio-for-mac"></a>在 Visual Studio for Mac 中生成 ASP.NET Core 应用程序

ASP.NET Core 是开放源跨平台框架，用于生成基于新式云的 Internet 连接应用程序，例如 Web 应用和服务、IoT 应用以及移动后端。 ASP.NET Core 应用可以在 [.NET Core](https://www.microsoft.com/net/core/platform) 或 .NET Framework 运行时上运行。 其设计目标是为部署到云或在本地运行的应用提供优化的开发框架。 该应用由模块化组件组成，开销最小，因此你可以在构造解决方案时保持灵活性。 可以在 Windows、Mac 和 Linux 上跨平台开发和运行 ASP.NET Core 应用。 ASP.NET Core 在 [GitHub](https://github.com/aspnet/home) 为开放源。

在本实验室中，你将使用 Visual Studio for Mac 创建并探索 ASP.NET Core 应用程序。

## <a name="objectives"></a>目标

> [!div class="checklist"]
> * 创建 ASP.NET Core Web 应用
> * 了解 ASP.NET Core 托管、配置和中间件模型
> * 调试 ASP.NET Core Web 应用

## <a name="prerequisites"></a>系统必备

- [Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac)

## <a name="intended-audience"></a>目标受众

本实验室适用于熟悉 C# 但不具有丰富经验的开发者。

## <a name="task-1-creating-a-new-aspnet-core-application"></a>任务 1：创建新的 ASP.NET Core 应用程序

1. 启动“Visual Studio for Mac”  。

2. 选择“文件”>“新建解决方案”  。

3. 依次选择“.NET Core”、“应用”类别和“ASP.NET Core Web 应用(C#)”模板   。 单击 **“下一步”** 。

    ![](media/netcore-image1.png)

4. 输入“CoreLab”的名称，然后单击“创建”，以创建项目   。 完成创建将需要一段时间。

    ![](media/netcore-image2.png)

## <a name="task-2-touring-the-solution"></a>任务 2：浏览解决方案

1. 默认模板生成的解决方案包含一个名为“CoreLab”的 ASP.NET Core 项目  。 展开项目节点，显示其内容。

    ![](media/netcore-image3.png)

2. 此项目遵循模型-视图-控制器 (MVC) 范例，清楚地划分数据（模型）、演示（视图）和功能（控制器）的职责。 从“控制器”  文件夹打开 HomeController.cs  文件。

    ![](media/netcore-image4.png)

3. HomeController 以按类约定的方式处理以 /Home 开头的所有传入请求   。 Index 方法处理针对目录根（如 `http://site.com/Home`）的请求，其他方法根据约定处理针对其命名路径的请求，例如 About() 处理对 `http://site.com/Home/About` 的请求。   当然，这些均可配置。 值得注意的是，HomeController 是新项目中的默认控制器，因此针对网站 (`http://site.com`) 的根的请求将贯穿 HomeController 的 Index()，就像针对 `http://site.com/Home` 或 `http://site.com/Home/Index` 的请求一样。   

    ![](media/netcore-image5.png)

4. 项目还有一个“视图”文件夹，其中包含映射到每个控制器的其他文件夹（以及一个“共享”视图的文件夹）   。 例如，/Home/About  路径的视图 CSHTML 文件（HTML 的扩展）将位于 **Views/Home/About.cshtml**。 打开该文件。

    ![](media/netcore-image6.png)

5. 此 CSHTML 文件使用 Razor 语法，基于标准标记和内联 C# 的组合来呈现 HTML。 [联机文档](https://docs.microsoft.com/aspnet/web-pages/overview/getting-started/introducing-razor-syntax-c)对此进行了详细介绍。

    ![](media/netcore-image7.png)

6. 解决方案还包含 wwwroot 文件夹，它是网站的根  。 部署站点时，可以直接将静态站点内容（如 CSS、映像和 JavaScript 库）置于所需路径。

    ![](media/netcore-image8.png)

7. 还有各种在运行时用来管理项目、包以及应用程序的配置文件。 例如，默认应用程序[配置](https://docs.microsoft.com/aspnet/core/fundamentals/configuration)存储在 appsettings.json  中。 但可以通过为“开发”  环境提供 appsettings.Development.json  文件之类的方式，基于每个环境替代部分/所有这些设置。

    ![](media/netcore-image9.png)

## <a name="task-3-understanding-how-the-application-is-hosted"></a>任务 3：了解如何托管应用程序

1. 在“解决方案资源管理器”中，打开 Program.cs   。 这是运行应用程序的引导程序。

    ![](media/netcore-image10.png)

2. 虽然此处只有两行代码，但这两行代码非常重要。 让我们将其拆开来看。 首先，创建新的 WebHostBuilder  。 ASP.NET Core 应用需要可在其中执行操作的主机。 主机必须实现 IWebHost 接口，该接口公开功能和服务的集合，以及 Start 方法   。 主机通常使用能够生成并返回 WebHost 实例的 WebHostBuilder 的实例创建   。 WebHost 引用将处理请求的服务器  。

    ![](media/netcore-image11.png)

3. 虽然 WebHostBuilder 负责创建为应用启动服务器的主机，但需要你提供实现 IServer 的服务器   。 默认情况下，这是跨平台 ASP.NET Core 跨平台 Web 服务器 [Kestrel](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel)，它基于跨平台异步 I/O 库 libuv   。

    ![](media/netcore-image12.png)

4. 接下来，设置服务器的内容根。 这决定搜索内容文件（如 MVC 视图文件）的位置。 默认内容根是在其中运行应用程序的文件夹。

    ![](media/netcore-image13.png)

5. 如果应用必须与 Internet Information Services (IIS) Web 服务器配合使用，则应在构建主机的过程中调用 UseIISIntegration 方法  。 这并不会配置服务器，而 UseKestrel 要配置  。 要将 IIS 与 ASP.NET Core 配合使用，必须同时指定 UseKestrel 和 UseIISIntegration   。 Kestrel 的设计目标是在代理后面运行，不应直接面向 Internet 部署  。 UseIISIntegration 将 IIS 指定为反向代理服务器，但只有在具有 IIS 的计算机上运行时才相关  。 如果将应用程序部署到 Windows，请将其保留在其中。 这不会造成损伤。

    ![](media/netcore-image14.png)

6. 将加载设置与应用程序启动分开，是一种更简洁的做法。 为方便起见，将调用 UseStartup 来指定调用 Startup 类，以完成设置加载和其他启动任务，例如将中间件插入 HTTP 管道   。 可能有多个 UseStartup 调用，并期望每个调用都会根据需要覆盖以前的设置  。

    ![](media/netcore-image15.png)

7. 创建 IWebHost 的最后一步是调用 Build   。

    ![](media/netcore-image16.png)

8. 虽然需要 IWebHost 类才能实现非阻止 Start，但 ASP.NET Core 项目具有名为 Run 的扩展方法，其中包含具有阻止代码的 Start，因此你无需手动阻止该方法立即退出     。

    ![](media/netcore-image17.png)

## <a name="task-4-running-and-debugging-the-application"></a>任务 4：运行和调试应用程序

1. 在“解决方案资源管理器”中，右键单击“CoreLab”项目节点，然后选择“选项”    。

    ![](media/netcore-image18.png)

2. “项目选项”对话框包含调整应用程序的生成和运行方式所需的一切  。 从左侧面板中依次选择“运行”、“配置”、“默认”节点  。

3. 选中“在外部控制台上运行”并取消选中“暂停控制台输出”   。 通常，自托管应用程序不会使其控制台可见，而是将其结果记录到“输出”板  。 出于本实验室的目的，我们也将在单独的窗口中显示控制台，但在正常开发过程中你不需要这样操作。

4. 单击 **“确定”** 。

    ![](media/netcore-image19.png)

5. 按 F5 生成并运行该应用程序  。 或者可以依次选择“运行”、“开始调试”  。

6. Visual Studio for Mac 将启动两个窗口。 第一个是控制台窗口，为你提供自托管服务器应用程序的视图。

    ![](media/netcore-image20.png)

7. 第二个是用于测试网站的典型浏览器窗口。 据浏览器的了解，可在任何地方托管此应用程序。 单击“关于”，导航至该页面  。

    ![](media/netcore-image21.png)

8. 此外，“关于”页面呈现在控制器中设置的一些文本。

    ![](media/netcore-image22.png)

9. 保持两个窗口处于打开状态并返回到 Visual Studio for Mac。 打开 Controllers/HomeController.cs  （如果尚未打开）。

    ![](media/netcore-image23.png)

10. 在 About 方法的第一行设置一个断点  。 可以通过单击边距或将光标置于行上并按 F9 来完成此操作  。 此行在 Views/Home/About.cshtml  处 CSHTML 页面中呈现的 ViewData  集合中设置一些数据。

    ![](media/netcore-image24.png)

11. 返回浏览器并刷新“关于”页面。 这会触发 Visual Studio for Mac 中的断点。

12. 将鼠标悬停在 ViewData 成员上，查看其数据  。 还可以展开其子成员，查看嵌套数据。

    ![](media/netcore-image25.png)

13. 使用用以添加断点的相同方式删除应用程序断点。

14. 打开 Views/Home/About.cshtml  。

15. 将文本“additional”  更改为“changed”  并保存文件。

    ![](media/netcore-image26.png)

16. 按“继续”按钮，继续执行操作  。

    ![](media/netcore-image27.png)

17. 返回浏览器窗口，查看更新的文本。 此更改可以在任何时间完成，并不一定需要调试程序断点。 如果未看到更改立即反映，请刷新浏览器。

    ![](media/netcore-image28.png)

18. 关闭测试浏览器窗口和应用程序控制台。 这也将停止调试。

## <a name="task-5-application-startup-configuration"></a>任务 5：应用程序启动配置

1. 在“解决方案资源管理器”中，打开 Startup.cs   。 最初你可能会注意到一些红色波浪线，因为 NuGet 包正在后台恢复，而 Roslyn 编译器正在构建完整的项目依赖关系。

    ![](media/netcore-image29.png)

2. 找到 Startup 方法  。 本部分定义应用程序的初始配置，并且非常紧凑。 让我们将其拆开来看。

    ![](media/netcore-image30.png)

3. 该方法首先初始化 ConfigurationBuilder 并设置其基本路径  。

    ![](media/netcore-image31.png)

4. 接下来，加载所需的 appsettings.json 文件  。

    ![](media/netcore-image32.png)

5. 之后，尝试加载环境特定的 appsettings.json 文件，这将覆盖现有设置  。 例如，这是提供用于该特定环境的 appsettings.Development.json 文件  。 要详细了解 ASP.NET Core 中的配置，请查看[文档](https://docs.microsoft.com/aspnet/core/fundamentals/configuration)。

    ![](media/netcore-image34.png)

6. 最后，将环境变量添加到配置生成器，生成配置并对其进行设置以供使用。

    ![](media/netcore-image35.png)

## <a name="task-6-inserting-application-middleware"></a>任务 6：插入应用程序中间件

1. 在 Startup 类中找到 Configure 方法   。 此方法可供配置所有中间件，这样可将其插入 HTTP 管道并用于处理针对服务器的每个请求。 虽然此方法只可调用一次，但方法的内容（例如 UseStaticFiles）可能会在每个请求中执行  。

    ![](media/netcore-image36.png)

2. 还可添加其他中间件，使其作为管道的一部分执行。 在 app.UseStaticFiles 之后添加以下代码，自动为每个传出响应添加 X-Test 标头   。 IntelliSense 将帮助在你键入时完成代码。

    ```csharp
    app.Use(async (context, next) =>
    {
        context.Response.Headers.Add("X-Test", new[] { "Test value" });
        await next();
    });
    ```

3. 按 F5  生成并运行项目。

4. 我们可以使用浏览器检查标头，验证是否已添加这些标头。 以下说明适用于 Safari，但你可以在 [Chrome](https://stackoverflow.com/questions/4423061/view-http-headers-in-google-chrome) 或 [Firefox](https://stackoverflow.com/questions/33974595/in-firefox-how-do-i-see-http-request-headers-where-in-web-console) 中执行相同的操作。

5. 浏览器加载网站后，即可依次选择“Safari”、“首选项”  。

6. 在“高级”选项卡上，选中“在菜单栏中显示开发菜单”，然后关闭对话框   。

    ![](media/netcore-image37.png)

7. 依次选择“开发”、“显示页面资源”  。

8. 刷新浏览器窗口，这样新打开的开发者工具可以跟踪并分析流量和内容。

9. 服务器呈现的 localhost HTML 页面将是默认选中的项目。

    ![](media/netcore-image38.png)

10. 展开“详细信息”边栏  。

    ![](media/netcore-image39.png)

11. 滚动到边栏底部，查看之前在代码中添加的响应标头。

    ![](media/netcore-image40.png)

12. 满意后关闭浏览器窗口和控制台。

## <a name="summary"></a>总结

在本实验室中，你已了解了如何使用 Visual Studio for Mac 开始开发 ASP.NET Core 应用。 如果你想探索开发更完整的电影数据库应用程序，请参阅 [ASP.NET Core MVC 入门](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc)教程。
