---
title: 将 ASP.NET Core Linux Docker 容器部署到 Azure 应用服务 | Microsoft Docs
description: 了解如何使用 Visual Studio 容器工具将 ASP.NET Core Web 应用部署到 Azure 应用服务
author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.devlang: dotnet
ms.topic: how-to
ms.date: 01/27/2020
ms.author: ghogen
ms.openlocfilehash: 43bd06fba795c09bfa341ce7b61a3ced0fe15214
ms.sourcegitcommit: 510a928153470e2f96ef28b808f1d038506cce0c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2020
ms.locfileid: "86454158"
---
# <a name="deploy-an-aspnet-core-container-to-azure-app-service-using-visual-studio"></a>使用 Visual Studio 将 ASP.NET Core 容器部署到 Azure 应用服务

本教程逐步介绍如何使用 Visual Studio 将容器化 ASP.NET Core Web 应用程序发布到 [ Azure 应用服务](/azure/app-service)。 Azure 应用服务是 Azure 中托管的单容器 Web 应用的相应服务。

如果没有 Azure 订阅，请在开始之前创建一个[免费帐户](https://azure.microsoft.com/free/dotnet/?utm_source=acr-publish-doc&utm_medium=docs&utm_campaign=docs)。

## <a name="prerequisites"></a>先决条件

完成本教程：

::: moniker range="vs-2017"
- 安装带有“ASP.NET 和 Web 开发”工作负载的最新版本 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)
::: moniker-end
::: moniker range=">=vs-2019"
- [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) 与“ASP.NET 和 Web 开发”工作负载。
::: moniker-end
- 安装 [Docker Desktop](https://docs.docker.com/docker-for-windows/install/)

## <a name="create-an-aspnet-core-web-app"></a>创建 ASP.NET Core Web 应用

以下步骤将指导你完成创建基本 ASP.NET Core 应用（将在本教程中使用）的过程。

::: moniker range="vs-2017"
1. 在 Visual Studio 菜单中，选择“文件”>“新建”>“项目”。
2. 在“新建项目”对话框的“模板”部分下，选择“Visual C#”>“Web”。
3. 选择“ASP.NET Core Web 应用程序”。
4. 为新应用程序指定名称（或使用默认值），并选择“确定”。
5. 选择“Web 应用程序”。
6. 勾选“启用 Docker 支持”复选框。
7. 选择“Linux”容器类型，然后单击“确定” 。 不支持将 Windows 容器作为容器部署到 Azure 应用服务。
::: moniker-end
::: moniker range=">= vs-2019"
1. 在 Visual Studio“启动”窗口，选择“创建新项目”。
1. 依次选择“ASP.NET Core Web 应用程序”和“下一步” 。
1. 为新应用程序指定名称（或使用默认名称），并选择“创建”。
1. 选择“Web 应用程序”。
1. 通过使用“为 HTTPS 配置”复选框，选择是否需要 SSL 支持。
1. 勾选“启用 Docker 支持”复选框。
1. 选择容器类型，然后单击“创建”。
::: moniker-end

## <a name="deploy-the-container-to-azure"></a>将容器部署到 Azure

::: moniker range="vs-2017"

1. 在解决方案资源管理器中右键单击项目，并选择“发布” 。
1. 在发布目标对话框中，选择“应用服务 Linux”或“应用服务” 。 这是将托管 Web 服务器的操作系统。
1. 可以只发布到应用服务，也可以发布到应用服务和 Azure 容器注册表 (ACR)。 若要将容器发布到 Azure 容器注册表 (ACR)，请选择“为容器创建新的应用服务”，并单击“发布” 。

   ![“发布”对话框的屏幕截图](media/deploy-app-service/publish-app-service-linux.PNG)

   若要在不使用 Azure 容器注册表的情况下仅发布到 Azure 应用服务，请选择“新建”，然后单击“发布” 。

1. 检查是否已使用与 Azure 订阅相关联的帐户登录，并选择唯一名称、订阅、资源组、托管计划和容器注册表（如果适用），或接受默认值。

   ![“发布”设置的屏幕截图](media/deploy-app-service/publish-app-service-linux2.png)

1. 选择“创建”。 容器将部署到 Azure 中你所选的资源组和容器注册表中。 此过程需要花费一些时间。 完成后，“发布”选项卡显示有关已发布内容的信息，包括网站 URL。

   ![“发布”选项卡的屏幕截图](media/deploy-app-service/publish-succeeded.PNG)

1. 单击“站点”链接，验证应用在 Azure 中是否按预期方式工作。

   ![Web 应用程序的屏幕截图](media/deploy-app-service/web-application-running.png)

1. 发布配置文件会保存你所选的所有详细信息，如资源组和容器注册表。

1. 若要使用相同的发布配置文件再次部署，请使用“发布”按钮、“Web 发布活动”窗口中的“发布”按钮，或在解决方案资源管理器中右键单击该项目，并在上下文菜单上选择“发布”项    。
:::moniker-end
:::moniker range=">=vs-2019"
1. 在解决方案资源管理器中右键单击项目，并选择“发布” 。
1. 在“发布”对话框中，选择“Azure”目标。

   ![“发布”向导的屏幕截图](media/deploy-app-service/publish-choices.png)

1. 在“特定目标”选项卡上，根据容器类型选择适当的部署目标，如“应用服务(Windows)”或“应用服务(Linux)”。

   ![“发布”向导的“特定目标”选项卡的屏幕截图](media/deploy-app-service/publish-app-service-windows.png)

1. 如果没有通过要使用的订阅登录正确的 Azure 帐户，请使用“发布”窗口左上角的按钮进行登录。

1. 可以使用现有的应用服务，也可以通过单击“新建 Azure 应用服务”链接来新建应用服务。 通过展开资源组来在树视图中查找现有应用服务，或将“视图”设置更改为“资源类型”来按类型排序。

   ![显示如何选择应用服务的屏幕截图](media/deploy-app-service/publish-app-service-windows2.png)

1. 如果新建应用服务，则会在 Azure 中生成资源组和应用服务。 如果需要，可以更改名称，只要它们是唯一的。

   ![显示如何创建应用服务的屏幕截图](media/deploy-app-service/publish-app-service-windows3.png)

1. 可以接受默认的托管计划，也可以在 Azure 门户中立即或稍后更改托管计划。 在受支持的区域之一，默认值为 `S1`（小）。 若要创建托管计划，请选择“托管计划”下拉列表旁边的“新建”。 此时，“托管计划”窗口显示。

   ![显示“托管计划”选项的屏幕截图](media/deploy-app-service/hosting-plan.png)

   若要详细了解这些选项，可以查看 [Azure 应用服务计划概述](/azure/app-service/overview-hosting-plans)。

1. 选择或创建完这些资源后，立即选择“完成”。 此时，容器部署到 Azure 中你所选的资源组和应用服务内。 此过程需要花费一些时间。 完成后，“发布”选项卡显示有关已发布内容的信息，包括网站 URL。

   ![“发布”选项卡的屏幕截图](media/deploy-app-service/publish-succeeded-windows.png)

1. 单击“站点”链接，验证应用在 Azure 中是否按预期方式工作。

   ![Web 应用程序的屏幕截图](media/deploy-app-service/web-application-running2.png)

1. 发布配置文件会保存你所选的全部详细信息，如资源组和应用服务。

1. 若要使用相同的发布配置文件再次部署，请使用“发布”按钮、“Web 发布活动”窗口中的“发布”按钮，或在解决方案资源管理器中右键单击该项目，并在上下文菜单上选择“发布”项    。
:::moniker-end

## <a name="view-container-settings"></a>查看容器设置

在 [Azure 门户](https://portal.azure.com)中，可以打开已部署的应用服务。

可以打开“容器设置”菜单来查看已部署应用服务的设置（如果使用的是 Visual Studio 2019 版本 16.4 或更高版本）。

![Azure 门户中的容器设置菜单的屏幕截图](media/deploy-app-service/container-settings-menu.png)

可以从此处查看容器信息、查看或下载日志记录或设置持续部署。 请参阅 [Azure 应用服务持续部署 CI/CD](/azure/app-service/containers/app-service-linux-ci-cd)。

## <a name="clean-up-resources"></a>清理资源

若要删除与本教程相关联的所有 Azure 资源，请使用 [Azure 门户](https://portal.azure.com)删除相应的资源组。 若要查找与已发布 Web 应用程序相关联的资源组，请选择“查看” > “其他 Windows” > “Web 发布活动”，然后选择齿轮图标  。 此时会打开“发布”选项卡，其中包含资源组。

在 Azure 门户中，选择“资源组”，选择要打开其详细信息页面的资源组。 确认这是正确的资源组，然后选择“删除资源组”，键入名称，并选择“删除” 。

## <a name="next-steps"></a>后续步骤

详细了解 [Azure 应用服务](/azure/app-service/overview)。

## <a name="see-also"></a>请参阅

[部署到 Azure 容器注册表](hosting-web-apps-in-docker.md)