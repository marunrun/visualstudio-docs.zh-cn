---
title: 教程 - 使用 Docker Compose 创建多容器应用
description: 了解如何在 Visual Studio for Mac 中管理多个容器并在它们之间通信
author: heiligerdankgesang
ms.author: dominicn
ms.date: 06/17/2019
ms.topic: tutorial
ms.openlocfilehash: 03adc2385c202710425fbc8e6b12c832526b5f90
ms.sourcegitcommit: 2ce59c2ffeba5ba7f628c2e6c75cba4731deef8a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2020
ms.locfileid: "85938942"
---
# <a name="create-a-multi-container-app-with-docker-compose"></a>使用 Docker Compose 创建多容器应用

在本教程中，你将了解如何在 Visual Studio for Mac 中使用 Docker Compose 管理多个容器并在它们之间通信。

## <a name="prerequisites"></a>先决条件

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
* [Visual Studio for Mac 2019](https://visualstudio.microsoft.com/vs/mac)

## <a name="create-an-aspnet-core-web-application-and-add-docker-support"></a>创建 ASP.NET Core Web 应用程序并添加 Docker 支持

1. 通过转到“文件”>“新建解决方案”  来创建新解决方案。
1. 在“.NET Core”>“应用”  下，选择“Web 应用程序”  模板：![创建新 ASP.NET 应用程序](media/docker-quickstart-1.png)
1. 选择目标框架。 本示例将使用 .NET Core 2.2：![设置目标框架](media/docker-quickstart-2.png)
1. 输入项目详细信息，例如项目名称（在此示例中为 _DockerDemoFrontEnd_）和解决方案名称 (_DockerDemo_)。 创建的项目包含生成并运行 ASP.NET Core Web 站点所需的所有基础知识。
1. 在 Solution Pad 中，右键单击 DockerDemoFrontEnd 项目，并选择“添加”>“添加 Docker 支持”  ：![添加 docker 支持](media/docker-quickstart-3.png)

Visual Studio for Mac 自动将新项目添加到名为 docker-compose  的解决方案，并将 Dockerfile  添加到现有项目。

## <a name="create-an-aspnet-core-web-api-and-add-docker-support"></a>创建 ASP.NET Core Web API 并添加 Docker 支持

接下来我们将创建第二个项目，其将充当后端 API。 .NET Core API  模板包括支持处理 RESTful 请求的控制器。

1. 通过右键单击解决方案并选择“添加”>“添加新项目”  ，将新项目添加到现有解决方案中。
1. 在“.NET Core”>“应用”  下，选择“API”  模板。
1. 选择目标框架。 本示例将使用 .NET Core 2.2
1. 输入项目详细信息，例如项目名称（在此示例中为 _DockerDemoAPI_）。
1. 创建后，转到“Solution Pad”，右键单击 DockerDemoAPI 项目并选择“添加”>“添加 Docker 支持”  。

docker-compose  项目中的 docker-compose.yml  文件将自动更新，以包含与现有 Web 应用项目一起的 API 项目。 当生成并运行 docker-compose  项目中，其中每个项目都将部署到单独的 Docker 容器。

```
version: '3.4'

services:
  dockerdemofrontend:
    image: ${DOCKER_REGISTRY-}dockerdemofrontend
    build:
      context: .
      dockerfile: DockerDemoFrontEnd/Dockerfile

  dockerdemoapi:
    image: ${DOCKER_REGISTRY-}dockerdemoapi
    build:
      context: .
      dockerfile: DockerDemoAPI/Dockerfile
```

## <a name="integrate-the-two-containers"></a>集成两个容器

现在我们的解决方案中有两个 ASP.NET 项目，二者都已配置为具有 Docker 支持。 接下来我们需要添加一些代码！

1. 在 `DockerDemoFrontEnd` 项目中，打开 Index.cshtml.cs  文件，使用以下代码替换 `OnGet` 方法：

   ```csharp
    public async Task OnGet()
    {
       ViewData["Message"] = "Hello from webfrontend";

       using (var client = new System.Net.Http.HttpClient())
       {
          // Call *mywebapi*, and display its response in the page
          var request = new System.Net.Http.HttpRequestMessage();
          request.RequestUri = new Uri("http://dockerdemoapi/api/values/1");
          var response = await client.SendAsync(request);
          ViewData["Message"] += " and " + await response.Content.ReadAsStringAsync();
       }
    }
   ```

1. 在 Index.cshtml  文件中，添加一行以显示 `ViewData["Message"]`，以便该文件看起来如以下代码：

      ```cshtml
      @page
      @model IndexModel
      @{
          ViewData["Title"] = "Home page";
      }

      <div class="text-center">
          <h1 class="display-4">Welcome</h1>
          <p>Learn about <a href="https://docs.microsoft.com/aspnet/core">building Web apps with ASP.NET Core</a>.</p>
          <p>@ViewData["Message"]</p>
      </div>
      ```

1. 现在在 Web API 项目中，将代码添加到“值”控制器以自定义 API 针对从 webfrontend  添加的调用返回的消息：

      ```csharp
        // GET api/values/5
        [HttpGet("{id}")]
        public ActionResult<string> Get(int id)
        {
            return "webapi (with value " + id + ")";
        }
      ```

1. 将 `docker-compose` 项目设置为启动项目并转到“运行”>“开始调试”  。 如果所有内容配置正确，你将看到消息“Hello from webfrontend and webapi (with value 1)”：

![Docker 多容器解决方案正在运行](media/docker-multicontainer-debug.png)
