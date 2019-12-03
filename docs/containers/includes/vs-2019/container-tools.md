---
title: 使用 ASP.NET Core 的 Visual Studio Tools for Docker
author: ghogen
description: 了解如何使用 Visual Studio 2019 工具和 Docker for Windows
ms.author: ghogen
ms.date: 02/01/2019
ms.prod: visual-studio-dev16
ms.technology: vs-azure
ms.topic: include
ms.openlocfilehash: 0232b37d08901bcc04c9d66facfe6850a9852e88
ms.sourcegitcommit: e825d1223579b44ee2deb62baf4de0153f99242a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2019
ms.locfileid: "74485485"
---
使用 Visual Studio，可以轻松地生成、调试和运行容器化的 .NET、ASP.NET 和 ASP.NET Core 应用并将其发布到 Azure 容器注册表 (ACR)、Docker Hub、Azure 应用服务或你自己的容器注册表。 本文介绍如何将 ASP.NET Core 应用发布到 ACR。

## <a name="prerequisites"></a>系统必备

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* 安装了“Web 开发”、“Azure 工具”工作负载和/或“.NET Core 跨平台开发”工作负载的 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)   
* 用于使用 .NET Core 2.2 进行开发的 [.NET Core 2.2 开发工具](https://dotnet.microsoft.com/download/dotnet-core/2.2)
* 若要发布到 Azure 容器注册表，需要 Azure 订阅。 [注册免费试用版](https://azure.microsoft.com/offers/ms-azr-0044p/)。

## <a name="installation-and-setup"></a>安装和设置

要安装 Docker，请先查看[用于 Windows 的 Docker Desktop：安装须知](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install)了解相关信息。 然后安装[用于 Windows 的 Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)。

## <a name="add-a-project-to-a-docker-container"></a>向 Docker 容器添加项目

1. 使用“ASP.NET Core Web 应用程序”  模板创建新项目。
1. 选择“Web 应用程序”，确保已选择“启用 Docker 支持”复选框   。

   ![“启用 Docker 支持”复选框](../../media/container-tools/vs-2019/create-new-web-application.PNG)

1. 选择所需的容器类型（Windows 或 Linux），然后单击“创建”  。

## <a name="dockerfile-overview"></a>Dockerfile 概述

Dockerfile，用于创建最终 Docker 映像的方案，已在项目中创建  。 请参阅 [Dockerfile 引用](https://docs.docker.com/engine/reference/builder/)，了解其中的命令：

```
FROM microsoft/dotnet:2.2-aspnetcore-runtime-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk-stretch AS build
WORKDIR /src
COPY ["HelloDockerTools/HelloDockerTools.csproj", "HelloDockerTools/"]
RUN dotnet restore "HelloDockerTools/HelloDockerTools.csproj"
COPY . .
WORKDIR "/src/HelloDockerTools"
RUN dotnet build "HelloDockerTools.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HelloDockerTools.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloDockerTools.dll"]
```

前面的 Dockerfile 基于 [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore/) 映像，并包括通过构建项目并将其添加到容器中修改基本映像的说明  。

如果选中了新建项目对话框的“为 HTTPS 配置”复选框，则 Dockerfile 公开两个端口   。 一个端口用于 HTTP 流量；另一个端口用于 HTTPS。 如果未选中该复选框，则为 HTTP 流量公开单个端口 (80)。

## <a name="debug"></a>调试

在工具栏的调试下拉列表中选择“Docker”  ，然后开始调试应用。 你可能会看到提示信任证书的消息；选择信任证书以继续。

“输出”  窗口中的“容器工具”  选项显示正在进行的操作。

## <a name="containers-window"></a>容器窗口

如果拥有 Visual Studio 2019 版本 16.4 或更高版本，则可使用“容器”窗口来查看正在计算机上运行的容器，还可查看你可用的映像  。

在 IDE 中使用搜索框打开“容器”窗口（按 Ctrl+Q 可进行使用），键入 `container`然后从列表中选择“容器”窗口     。

可将“容器”窗口四处移动并沿着窗口放置参考线操作，将此窗口装载到便利的位置，例如在编辑器下方  。

在窗口中，找到你的容器并逐个浏览每个选项卡，以查看环境变量、端口映射、日志和文件系统。

![“容器”窗口的屏幕截图](../../media/overview/vs-2019/container-tools-window.png)

有关详细信息，请参阅[在 Visual Studio 中查看和诊断容器及映像](../../view-and-diagnose-containers.md)。

## <a name="publish-docker-images"></a>发布 Docker 映像

完成应用程序的开发和调试循环后，可以创建应用程序的生产映像。

1. 将配置下拉列表更改为“发布”  ，然后生成应用。
1. 在解决方案资源管理器中右键单击项目，并选择“发布”   。
1. 在发布目标对话框上，选择“容器注册表”选项卡  。
1. 选择“创建新的 Azure 容器注册表”并单击“发布”   。
1. 在“创建新 Azure 容器注册表”中填写所需的值  。

    | 设置      | 建议的值  | 说明                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **DNS 前缀** | 全局唯一名称 | 用于唯一标识容器注册表的名称。 |
    | **订阅** | 选择订阅 | 要使用的 Azure 订阅。 |
    | **[资源组](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  要在其中创建容器注册表的资源组的名称。 选择“新建”  创建新的资源组。|
    | **[SKU](https://docs.microsoft.com/azure/container-registry/container-registry-skus)** | 标准 | 容器注册表的服务层  |
    | **注册表位置** | 靠近你的位置 | 在你附近或将使用容器注册表的其他服务附近的[区域](https://azure.microsoft.com/regions/)中，选择位置。 |

    ![Visual Studio 的创建 Azure 容器注册表对话框][0]

1. 单击“创建” 

   ![显示成功发布的屏幕截图](../../media/container-tools/publish-succeeded.png)

## <a name="next-steps"></a>后续步骤

现在可以将容器从注册表中拖放到任何能够运行 Docker 映像的主机上，例如[Azure 容器实例](/azure/container-instances/container-instances-tutorial-deploy-app)。

[0]:../../media/hosting-web-apps-in-docker/vs-acr-provisioning-dialog-2019.png
