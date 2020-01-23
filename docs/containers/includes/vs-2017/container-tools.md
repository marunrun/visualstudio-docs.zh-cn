---
title: 带有 ASP.NET Core 的 Visual Studio 容器工具
author: ghogen
description: 了解如何使用 Visual Studio 2017 工具和 Docker for Windows
ms.author: ghogen
ms.date: 02/01/2019
ms.technology: vs-azure
ms.topic: include
ms.openlocfilehash: 63d2f021aabc3d9152900ad62f072ec1a35a8e5b
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75927933"
---
使用 Visual Studio，可以轻松地生成、调试和运行容器化的 ASP.NET Core 应用程序并将其发布到 Azure 容器注册表 (ACR)、Docker Hub、Azure 应用服务或你自己的容器注册表。 在本文中，我们将发布到 ACR。

## <a name="prerequisites"></a>先决条件

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* 安装了“Web 开发”、“Azure 工具”工作负载和/或“.NET Core 跨平台开发”工作负载的 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)   
* 若要发布到 Azure 容器注册表，需要 Azure 订阅。 [注册免费试用版](https://azure.microsoft.com/offers/ms-azr-0044p/)。

## <a name="installation-and-setup"></a>安装和设置

要安装 Docker，请先查看[用于 Windows 的 Docker Desktop：安装须知](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install)了解相关信息。 然后安装[用于 Windows 的 Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)。

## <a name="add-a-project-to-a-docker-container"></a>向 Docker 容器添加项目

1. 在 Visual Studio 菜单中，选择“文件”>“新建”>“项目”。 
1. 在“新建项目”对话框的“模板”部分下，选择“Visual C#”>“Web”。   
1. 选择“ASP.NET Core Web 应用程序”  。
1. 为新应用程序指定名称（或使用默认值），并选择“确定”。 
1. 选择“Web 应用程序”  。
1. 勾选“启用 Docker 支持”复选框  。

   ![“启用 Docker 支持”复选框](../../media/container-tools/enable-docker-support.PNG)

1. 选择所需的容器类型（Windows 或 Linux），然后单击“确定”  。

## <a name="dockerfile-overview"></a>Dockerfile 概述

Dockerfile，用于创建最终 Docker 映像的方案，已在项目中创建  。 请参阅 [Dockerfile 引用](https://docs.docker.com/engine/reference/builder/)，了解其中的命令：

```
FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 59518
EXPOSE 44364

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY HelloDockerTools/HelloDockerTools.csproj HelloDockerTools/
RUN dotnet restore HelloDockerTools/HelloDockerTools.csproj
COPY . .
WORKDIR /src/HelloDockerTools
RUN dotnet build HelloDockerTools.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish HelloDockerTools.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloDockerTools.dll"]
```

前面的 Dockerfile 基于 [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore/) 映像，并包括通过构建项目并将其添加到容器中修改基本映像的说明  。

如果选中了新建项目对话框的“为 HTTPS 配置”复选框，则 Dockerfile 公开两个端口   。 一个端口用于 HTTP 流量；另一个端口用于 HTTPS。 如果未选中该复选框，则为 HTTP 流量公开单个端口 (80)。

## <a name="debug"></a>调试

在工具栏的调试下拉列表中选择“Docker”  ，然后开始调试应用。 你可能会看到提示信任证书的消息；选择信任证书以继续。

“输出”窗口显示正在进行的操作  。

依次选择“工具”菜单 >“NuGet 包管理器”>“包管理器控制台”，打开包管理器控制台 (PMC)    。

最终得到的应用的 Docker 映像标记为“开发”  。 该映像基于 microsoft/dotnet 基础映像的 2.1-aspnetcore-runtime 标记   。 在“包管理器控制台”(PMC) 窗口中运行 `docker images` 命令  。 显示了计算机上的映像：

```console
REPOSITORY        TAG                     IMAGE ID      CREATED         SIZE
hellodockertools  dev                     d72ce0f1dfe7  30 seconds ago  255MB
microsoft/dotnet  2.1-aspnetcore-runtime  fcc3887985bb  6 days ago      255MB
```

> [!NOTE]
> “开发”映像不包含应用程序二进制文件和其他内容，因为“调试”配置使用卷装载提供迭代编辑和调试体验   。 若要创建包含所有内容的生产映像，请使用“版本”配置  。

在 PMC 中运行 `docker ps` 命令。 请注意，应用使用容器运行：

```console
CONTAINER ID        IMAGE                  COMMAND                   CREATED             STATUS              PORTS                   NAMES
baf9a678c88d        hellodockertools:dev   "C:\\remote_debugge..."   21 seconds ago      Up 19 seconds       0.0.0.0:37630->80/tcp   dockercompose4642749010770307127_hellodockertools_1
```

## <a name="publish-docker-images"></a>发布 Docker 映像

完成应用程序的开发和调试循环后，可以创建应用程序的生产映像。

1. 将配置下拉列表更改为“发布”  ，然后生成应用。
1. 在解决方案资源管理器中右键单击项目，并选择“发布”   。
1. 在发布目标对话框上，选择“容器注册表”选项卡  。
1. 选择“创建新的 Azure 容器注册表”并单击“发布”   。
1. 在“创建新 Azure 容器注册表”中填写所需的值  。

    | 设置      | 建议的值  | 描述                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **DNS 前缀** | 全局唯一名称 | 用于唯一标识容器注册表的名称。 |
    | **订阅** | 选择订阅 | 要使用的 Azure 订阅。 |
    | **[资源组](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  要在其中创建容器注册表的资源组的名称。 选择“新建”  创建新的资源组。|
    | **[SKU](/azure/container-registry/container-registry-skus)** | 标准 | 容器注册表的服务层  |
    | **注册表位置** | 靠近你的位置 | 在你附近或将使用容器注册表的其他服务附近的[区域](https://azure.microsoft.com/regions/)中，选择位置。 |

    ![Visual Studio 的创建 Azure 容器注册表对话框][0]

1. 单击“创建” 

## <a name="next-steps"></a>后续步骤

现在可以将容器从注册表中拖放到任何能够运行 Docker 映像的主机上，例如[Azure 容器实例](/azure/container-instances/container-instances-tutorial-deploy-app)。

[0]:../../media/hosting-web-apps-in-docker/vs-acr-provisioning-dialog.png
