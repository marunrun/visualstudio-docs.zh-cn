---
title: 使用 Docker Compose 与 ASP.NET Core 的多容器教程
author: ghogen
description: 了解如何将多个容器与 Docker Compose 配合使用
ms.author: ghogen
ms.date: 01/10/2020
ms.technology: vs-azure
ms.topic: include
ms.openlocfilehash: b9e1a2fc7c9027c34aeb8a0e0d1d44fdb0211e65
ms.sourcegitcommit: b2fc9ac7d73c847508f6ed082bed026476bb3955
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2020
ms.locfileid: "77027335"
---
# <a name="tutorial-create-a-multi-container-app-with-docker-compose"></a>教程：使用 Docker Compose 创建多容器应用

本教程介绍如何在 Visual Studio 中使用容器工具管理多个容器并在容器之间通信。  管理多个容器需要容器业务流程，并需要 Docker Compose、Kubernetes 或 Service Fabric 等业务流程协调程序  。 我们将在这里使用 Docker Compose。 Docker Compose 非常适用于开发周期中的本地调试和测试。

## <a name="prerequisites"></a>先决条件

::: moniker range="vs-2017"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* 安装了“Web 开发”、“Azure 工具”工作负载或“.NET Core 跨平台开发”工作负载的 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)   
::: moniker-end

::: moniker range=">= vs-2019"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* 安装了“Web 开发”、“Azure 工具”工作负载和/或“.NET Core 跨平台开发”工作负载的 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)   
* 用于使用 .NET Core 2.2 进行开发的 [.NET Core 2.2 开发工具](https://dotnet.microsoft.com/download/dotnet-core/2.2)
* 用于使用 .NET Core 3.1 进行开发的 [.NET Core 3 开发工具](https://dotnet.microsoft.com/download/dotnet-core/3.1)。
::: moniker-end

## <a name="create-a-web-application-project"></a>创建 Web 应用程序项目

在 Visual Studio 中，创建 ASP.NET Core web 应用程序项目，将其命名为 `WebFrontEnd`  。 选择“Web 应用程序”，以创建使用 Razor Pages 的 Web 应用程序  。 
  
::: moniker range="vs-2017"

请不要选择“启用 Docker 支持”  。 稍后添加 Docker 支持。

![创建 Web 项目的屏幕截图](./media/tutorial-multicontainer/docker-tutorial-enable-docker-support.png)

::: moniker-end

::: moniker range="vs-2019"

![创建 Web 项目的屏幕截图](./media/tutorial-multicontainer/vs-2019/new-aspnet-core-project1.png)

请不要选择“启用 Docker 支持”  。 稍后添加 Docker 支持。

![创建 Web 项目的屏幕截图](./media/tutorial-multicontainer/vs-2019/new-aspnet-core-project.png)

::: moniker-end

## <a name="create-a-web-api-project"></a>创建 Web API 项目

将项目添加到同一解决方案中，并将其称为 MyWebAPI  。 对于“项目类型”，选择“API”，并清除“HTTPS 配置”复选框   。 在此设计中，我们仅将 SSL 用于客户端通信，而不用于在同一个 Web 应用程序中的容器之间进行通信。 只有 `WebFrontEnd` 需要 HTTPS，且示例中的代码假定你已清除该复选框。

::: moniker range="vs-2017"
   ![创建 Web API 项目的屏幕截图](./media/tutorial-multicontainer/docker-tutorial-mywebapi.png)
::: moniker-end
::: moniker range="vs-2019"
   ![创建 Web API 项目的屏幕截图](./media/tutorial-multicontainer/vs-2019/web-api-project.png)
::: moniker-end

## <a name="add-code-to-call-the-web-api"></a>添加用于调用 Web API 的代码

1. 在 `WebFrontEnd` 项目中，打开 Index.cshtml.cs 文件，使用以下代码替换 `OnGet` 方法  。

   ```csharp
    public async Task OnGet()
    {
       ViewData["Message"] = "Hello from webfrontend";

       using (var client = new System.Net.Http.HttpClient())
       {
          // Call *mywebapi*, and display its response in the page
          var request = new System.Net.Http.HttpRequestMessage();
          // request.RequestUri = new Uri("http://mywebapi/WeatherForecast"); // ASP.NET 3 (VS 2019 only)
          request.RequestUri = new Uri("http://mywebapi/api/values/1"); // ASP.NET 2.x
          var response = await client.SendAsync(request);
          ViewData["Message"] += " and " + await response.Content.ReadAsStringAsync();
       }
    }
   ```
   
    > [!NOTE]
    > 在实际的代码中，不应在每次请求后释放 `HttpClient`。 有关最佳做法，请参阅[使用 HttpClientFactory 实现复原 HTTP 请求](https://docs.microsoft.com/dotnet/architecture/microservices/implement-resilient-applications/use-httpclientfactory-to-implement-resilient-http-requests)。

   对于 Visual Studio 2019 或更高版本中的 .NET Core 3.1，Web API 模板使用 WeatherForecast API，因此请取消注释该行，并注释掉 ASP.NET 2.x 行。

1. 在 Index.cshtml  文件中，添加一行以显示 `ViewData["Message"]`，以便该文件看起来如以下代码：
    
      ```cshtml
      @page
      @model IndexModel
      @{
          ViewData["Title"] = "Home page";
      }
    
      <div class="text-center">
          <h1 class="display-4">Welcome</h1>
          <p>Learn about <a href="/aspnet/core">building Web apps with ASP.NET Core</a>.</p>
          <p>@ViewData["Message"]</p>
      </div>
      ```

1. （仅限 ASP.NET 2.x）现在在 Web API 项目中，将代码添加到“值”控制器以自定义 API 针对从 webfrontend  添加的调用返回的消息。
    
      ```csharp
        // GET api/values/5
        [HttpGet("{id}")]
        public ActionResult<string> Get(int id)
        {
            return "webapi (with value " + id + ")";
        }
      ```

    使用 .NET Core 3.1 则不需要执行此操作，因为你可以使用已存在的 WeatherForecast API。 但是，你需要在 Startup.cs 的 `Configure` 方法中注释掉对 <xref:Microsoft.AspNetCore.Builder.HttpsPolicyBuilderExtensions.UseHttpsRedirection*> 的调用，因为此代码使用 HTTP 而不是 HTTPS 来调用 Web API  。

    ```csharp
                //app.UseHttpsRedirection();
    ```

1. 在 `WebFrontEnd` 项目中，依次选择“添加”、“容器业务流程协调程序支持”  。 此时显示“Docker 支持选项”对话框  。

1. 选择“Docker Compose”  。

1. 选择目标操作系统，例如 Linux。

   ![选择目标操作系统的屏幕截图](media/tutorial-multicontainer/docker-tutorial-docker-support-options.PNG)

   Visual Studio 会在解决方案中的“docker-compose”节点上创建 docker-compose.yml 文件和 .dockerignore 文件，该项目以粗体字体显示，表明其为启动项目    。

   ![添加了 docker-compose 项目的解决方案资源管理器的屏幕截图](media/tutorial-multicontainer/multicontainer-solution-explorer.png)

   显示 docker-compose.yml，如下所示  ：

   ```yaml
   version: '3.4'

    services:
      webfrontend:
        image: ${DOCKER_REGISTRY-}webfrontend
        build:
          context: .
          dockerfile: WebFrontEnd/Dockerfile
   ```

   .dockerignore 文件包含你不希望 Docker 在容器中包含的文件类型和扩展名  。 这些文件通常与开发环境和源代码管理相关联，并不属于正在开发的应用或服务。

   查看“输出”窗格的“容器工具”部分，深入了解正在运行的命令  。  可看到命令行工具 docker-compose 用于配置和创建运行时容器。

1. 在 Web API 项目中，再次右键单击项目节点，然后选择“添加” > “容器业务流程协调程序支持”   。 选择“Docker Compose”，然后选择相同的目标操作系统  。  

    > [!NOTE]
    > 在此步中，Visual Studio 会创建 Dockerfile。 如果对已具有 Docker 支持的项目执行此操作，系统将提示是否要覆盖现有的 Dockerfile。 如果已在 Dockerfile 中进行了所需的更改，请选择“否”。

    Visual Studio 对 docker compose YML 文件进行一些更改。 现在，这两项服务都包括在内。

    ```yaml
    version: '3.4'
    
    services:
      webfrontend:
        image: ${DOCKER_REGISTRY-}webfrontend
        build:
          context: .
          dockerfile: WebFrontEnd/Dockerfile
    
      mywebapi:
        image: ${DOCKER_REGISTRY-}mywebapi
        build:
          context: .
          dockerfile: MyWebAPI/Dockerfile
    ```

1. 立即在本地运行站点（按 F5 或 Ctrl+F5），验证站点是否按预期方式工作。 如果 .NET Core 2.x 版本中的所有内容配置正确，你将看到消息“来自 webfrontend 和 webapi 的问候(值为 1)。”  通过 .NET Core 3，可以看到天气预测数据。

   添加容器业务流程时使用的第一个项目设置为在运行或调试时启动。 可以在 docker-compose 项目的“项目属性”中配置启动操作  。  在 docker-compose 项目节点上，右键单击以打开上下文菜单，然后选择“属性”，或使用 Alt+Enter  。  以下屏幕截图显示需要解决方案在此使用的属性。  例如，可以通过自定义“服务 URL”属性来更改已加载的页面  。

   ![docker-compose 项目属性的屏幕截图](media/tutorial-multicontainer/launch-action.png)

   下面是启动时看到的内容（.NET Core 2.x 版本）：

   ![正在运行的 Web 应用的屏幕截图](media/tutorial-multicontainer/webfrontend.png)

   适用于 .NET 3.1 的 Web 应用显示 JSON 格式的天气数据。

## <a name="next-steps"></a>后续步骤

查看用于[将容器部署到 Azure](/azure/containers) 的选项。

## <a name="see-also"></a>请参阅
  
[Docker Compose](https://docs.docker.com/compose/)  
[容器工具](/visualstudio/containers/)
