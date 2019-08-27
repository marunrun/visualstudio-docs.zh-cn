---
title: Docker 入门
description: 了解如何在 Visual Studio for Mac 中将 Docker 添加到你的项目
author: asb3993
ms.author: amburns
ms.date: 06/17/2019
ms.openlocfilehash: b456b3d285c167f97570c39d9eb6fd1abfc27e45
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68872165"
---
# <a name="get-started-with-docker-in-visual-studio-for-mac"></a>Visual Studio for Mac 中的 Docker 入门

使用 Visual Studio for Mac，可以轻松地生成、调试和运行容器化 ASP.NET Core 应用并将其发布到 Azure。

## <a name="prerequisites"></a>系统必备

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
* [Visual Studio for Mac 2019](https://visualstudio.microsoft.com/vs/mac)

## <a name="installation-and-setup"></a>安装和设置

对于 Docker 安装，请查看并遵循[安装适用于 Mac 的 Docker Desktop](https://docs.docker.com/docker-for-mac/install/) 中的信息。

## <a name="creating-an-aspnet-core-web-application-and-adding-docker-support"></a>创建 ASP.NET Core Web 应用程序并添加 Docker 支持

1. 通过转到“文件”>“新建解决方案”  来创建新解决方案。
1. 在“.NET Core”>“应用”  下，选择“Web 应用程序”  模板：![创建新 ASP.NET 应用程序](media/docker-quickstart-1.png)
1. 选择目标框架。 本示例将使用 .NET Core 2.2：![设置目标框架](media/docker-quickstart-2.png)
1. 输入项目详细信息，例如名称（在此示例中为 _DockerDemo_）。 创建的项目包含生成并运行 ASP.NET Core Web 站点所需的所有基础知识。
1. 在 Solution Pad 中，右键单击 DockerDemo 项目并选择“添加”>“添加 Docker 支持”  ：![添加 Docker 支持](media/docker-quickstart-3.png)

Visual Studio for Mac 自动将新项目添加到名为 docker-compose  的解决方案，并将 Dockerfile  添加到现有项目。

![生成的 docker 支持文件](media/docker-quickstart-4.png)

## <a name="dockerfile-overview"></a>Dockerfile 概述

Dockerfile 是指用于创建最终 Docker 映像的方案。 请参阅 [Dockerfile 引用](https://docs.docker.com/engine/reference/builder/)，了解其中的命令。

```
FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY DockerDemo/DockerDemo.csproj DockerDemo/
RUN dotnet restore DockerDemo/DockerDemo.csproj
COPY . .
WORKDIR /src/DockerDemo
RUN dotnet build DockerDemo.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish DockerDemo.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerDemo.dll"]
```

前面的 Dockerfile 基于 [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore/) 映像，并包括通过构建项目并将其添加到容器中修改基本映像的说明  。

> [!NOTE]
> Visual Studio for Mac 创建的默认 Dockerfile 公开端口 80 用于传输 HTTP 流量。 若要启用 HTTPS 流量，请将 `Expose 443` 添加到 Dockerfile。

## <a name="debugging"></a>调试

将 `docker-compose` 项目设置为启动项目并开始调试（“运行”>“开始调试”  ）。 这将在容器中生成、部署和启动 ASP.NET 项目。

> [!TIP]
> 安装 Docker Desktop 后首次运行时，在尝试进行调试时可能会收到以下错误：`Cannot start service dockerdemo: Mounts denied`
>
> 将 `/usr/local/share/dotnet/sdk/NuGetFallbackFolder` 添加到 Docker Desktop 中的“文件共享”选项卡：
>
> ![将 NuGetFallbackFolder 文件夹添加到“文件共享”](media/docker-quickstart-5.png)

生成完成后，将在 Safari 中启动应用程序：

![在 Safari 中运行的默认 Docker 项目](media/docker-quickstart-6.png)

请注意，容器将侦听某个端口（例如 `http://localhost:32768`），此端口可能会有所不同。

若要查看正在运行的容器的列表，请在终端使用 `docker ps` 命令。

请注意以下屏幕截图中的端口中继（在 PORTS  下）。 这显示了该容器正在侦听我们在上面的 Safari 中看到的端口，并将请求中继到端口 80（在 Dockerfile 中定义）上的内部 Web 服务器。 从应用程序的角度来看，它正在侦听端口 80：

![Docker 容器列表](media/docker-quickstart-7.png)
