---
title: 将 ASP.NET Core Linux Docker 容器部署到 Azure 应用服务 | Microsoft Docs
description: 了解如何使用 Visual Studio 容器工具将 ASP.NET Core Web 应用部署到 Azure 应用服务
author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.devlang: dotnet
ms.topic: article
ms.date: 03/08/2019
ms.author: ghogen
ms.openlocfilehash: 5d1f160435fd8c62a44d3e5d3192870143558de4
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73188789"
---
# <a name="deploy-an-aspnet-core-container-to-azure-app-service-using-visual-studio"></a>使用 Visual Studio 将 ASP.NET Core 容器部署到 Azure 应用服务

本教程逐步介绍如何使用 Visual Studio 将容器化 ASP.NET Core Web 应用程序发布到 [ Azure 应用服务](/azure/app-service)。 Azure 应用服务是 Azure 中托管的单容器 Web 应用的相应服务。

如果没有 Azure 订阅，请在开始之前创建一个[免费帐户](https://azure.microsoft.com/free/dotnet/?utm_source=acr-publish-doc&utm_medium=docs&utm_campaign=docs)。

## <a name="prerequisites"></a>系统必备

完成本教程：

::: moniker range="vs-2017"
- 安装带有“ASP.NET 和 Web 开发”工作负载的最新版本 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)
::: moniker-end
::: moniker range=">=vs-2019"
- 带有 ASP.NET 和 Web 开发  工作负荷的 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)。
::: moniker-end
- 安装 [Docker Desktop](https://docs.docker.com/docker-for-windows/install/)

## <a name="create-an-aspnet-core-web-app"></a>创建 ASP.NET Core Web 应用

以下步骤将指导你完成创建基本 ASP.NET Core 应用（将在本教程中使用）的过程。

::: moniker range="vs-2017"
1. 在 Visual Studio 菜单中，选择“文件”>“新建”>“项目”。 
2. 在“新建项目”对话框的“模板”部分下，选择“Visual C#”>“Web”。   
3. 选择“ASP.NET Core Web 应用程序”  。
4. 为新应用程序指定名称（或使用默认值），并选择“确定”。 
5. 选择“Web 应用程序”  。
6. 勾选“启用 Docker 支持”复选框  。
7. 选择“Linux”容器类型，然后单击“确定”   。 不支持将 Windows 容器作为容器部署到 Azure 应用服务。
::: moniker-end
::: moniker range=">= vs-2019"
1. 在 Visual Studio“启动”窗口，选择“创建新项目”  。
1. 依次选择“ASP.NET Core Web 应用程序”和“下一步”   。
1. 为新应用程序指定名称（或使用默认名称），并选择“创建”  。
1. 选择“Web 应用程序”  。
1. 通过使用“为 HTTPS 配置”复选框，选择是否需要 SSL 支持  。
1. 勾选“启用 Docker 支持”复选框  。
1. 选择“Linux”容器类型，然后单击“创建”   。 不支持将 Windows 容器作为容器部署到 Azure 应用服务。
::: moniker-end

## <a name="deploy-the-container-to-azure"></a>将容器部署到 Azure

1. 在解决方案资源管理器中右键单击项目，并选择“发布”   。
1. 在“发布目标”对话框中，选择“应用服务 Linux”  。
1. 可以只发布到应用服务，也可以发布到应用服务和 Azure 容器注册表 (ACR)。 若要将容器发布到 Azure 容器注册表 (ACR)，请选择“为容器创建新的应用服务”，并单击“发布”   。

   ![“发布”对话框的屏幕截图](media/deploy-app-service/publish-app-service-linux.PNG)

   若要在不使用 Azure 容器注册表的情况下仅发布到 Azure 应用服务，请选择“新建”，然后单击“发布”   。

1. 检查是否已使用与 Azure 订阅相关联的帐户登录，并选择唯一名称、订阅、资源组、托管计划和容器注册表（如果适用），或接受默认值。

   ![“发布”设置的屏幕截图](media/deploy-app-service/publish-app-service-linux2.png)

1. 选择“创建”。  容器将部署到 Azure 中你所选的资源组和容器注册表中。 此过程需要花费一些时间。 完成后，“发布”选项卡显示有关已发布内容的信息，包括网站 URL  。

   ![“发布”选项卡的屏幕截图](media/deploy-app-service/publish-succeeded.PNG)

1. 单击“站点”链接，验证应用在 Azure 中是否按预期方式工作。

   ![Web 应用程序的屏幕截图](media/deploy-app-service/web-application-running.png)

1. 发布配置文件会保存你所选的所有详细信息，如资源组和容器注册表。
1. 若要使用相同的发布配置文件再次部署，请使用“发布”按钮、“Web 发布活动”窗口中的“发布”按钮，或在解决方案资源管理器中右键单击该项目，并在上下文菜单上选择“发布”项      。

## <a name="clean-up-resources"></a>清理资源

若要删除与本教程相关联的所有 Azure 资源，请使用 [Azure 门户](https://portal.azure.com)删除相应的资源组。 若要查找与已发布 Web 应用程序相关联的资源组，请选择“查看” > “其他 Windows” > “Web 发布活动”，然后选择齿轮图标    。 此时会打开“发布”选项卡，其中包含资源组  。

在 Azure 门户中，选择“资源组”，选择要打开其详细信息页面的资源组  。 确认这是正确的资源组，然后选择“删除资源组”，键入名称，并选择“删除”   。

## <a name="next-steps"></a>后续步骤

使用 [Azure Pipelines](/azure/devops/pipelines/?view=azure-devops) 设置持续集成和持续交付 (CI/CD)。

## <a name="see-also"></a>请参阅

[部署到 Azure 容器注册表](hosting-web-apps-in-docker.md)