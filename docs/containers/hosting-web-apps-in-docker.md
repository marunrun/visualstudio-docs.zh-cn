---
title: 将 ASP.NET Docker 容器部署到 ACR 注册表
description: 了解如何使用 Visual Studio 容器工具将 ASP.NET 或 ASP.NET Core Web 应用部署到容器注册表
author: ghogen
manager: jillfra
ms.assetid: e5e81c5e-dd18-4d5a-a24d-a932036e78b9
ms.devlang: dotnet
ms.topic: how-to
ms.technology: vs-azure
ms.date: 03/14/2019
ms.author: ghogen
ms.openlocfilehash: 4626b64f5e733fec049d56dfe53407cc0fe31566
ms.sourcegitcommit: 2c26d6e6f2a5c56ae5102cdded7b02f2d0fd686c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2020
ms.locfileid: "88168681"
---
# <a name="deploy-an-aspnet-container-to-a-container-registry-using-visual-studio"></a>使用 Visual Studio 将 ASP.NET 容器部署到容器注册表

## <a name="overview"></a>概述

Docker 是轻型容器引擎，在某些方面类似于虚拟机，可以将其用于托管应用程序和服务。
本教程介绍如何使用 Visual Studio 将容器化应用程序发布到 [ Azure 容器注册表](https://azure.microsoft.com/services/container-registry)。

如果没有 Azure 订阅，请在开始之前创建一个[免费帐户](https://azure.microsoft.com/free/dotnet/?utm_source=acr-publish-doc&utm_medium=docs&utm_campaign=docs)。

## <a name="prerequisites"></a>先决条件

完成本教程：

::: moniker range="vs-2017"
* 安装带有“ASP.NET 和 Web 开发”工作负载的最新版本 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)
::: moniker-end
::: moniker range=">=vs-2019"
* 安装带有“ASP.NET 和 Web 开发”工作负载的最新版本 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)
::: moniker-end
* 安装[适用于 Windows 的 Docker](https://docs.docker.com/docker-for-windows/install/)

## <a name="create-an-aspnet-core-web-app"></a>创建 ASP.NET Core Web 应用

以下步骤将指导你完成创建基本 ASP.NET Core 应用（将在本教程中使用）的过程。 如果你已有一个项目，则可跳过此部分。

::: moniker range="vs-2017"
[!INCLUDE [create-aspnet5-app](../azure/includes/create-aspnet5-app.md)]
::: moniker-end
::: moniker range=">=vs-2019"
[!INCLUDE [create-aspnet5-app](../azure/includes/vs-2019/create-aspnet5-app-2019.md)]
::: moniker-end

::: moniker range="vs-2017"

## <a name="publish-your-container-to-azure-container-registry"></a>将容器发布到 Azure 容器注册表

1. 在解决方案资源管理器中右键单击项目，并选择“发布”   。
2. 在“发布目标”对话框中，选择“容器注册表” 。
3. 选择“新建 Azure 容器注册表”并单击“发布”   。
4. 在“创建新 Azure 容器注册表”中填写所需的值  。

    | 设置      | 建议的值  | 描述                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **DNS 前缀** | 全局唯一名称 | 用于唯一标识容器注册表的名称。 |
    | **订阅** | 选择订阅 | 要使用的 Azure 订阅。 |
    | **[资源组](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  要在其中创建容器注册表的资源组的名称。 选择“新建”  创建新的资源组。|
    | **[SKU](/azure/container-registry/container-registry-skus)** | 标准 | 容器注册表的服务层  |
    | **注册表位置** | 靠近你的位置 | 在你附近或将使用容器注册表的其他服务附近的[区域](https://azure.microsoft.com/regions/)中，选择位置。 |

    ![Visual Studio 的创建 Azure 容器注册表对话框](media/hosting-web-apps-in-docker/vs-acr-provisioning-dialog.png)

5. 单击“创建” 
::: moniker-end

::: moniker range=">=vs-2019"
## <a name="publish-your-container-to-azure-container-registry"></a>将容器发布到 Azure 容器注册表
1. 在解决方案资源管理器中右键单击项目，并选择“发布” 。
2. 在“发布”对话框中，选择“Docker 容器注册表” 。

   ![“‘发布’对话框 - 选择‘Docker 容器注册表’”的屏幕截图](media/container-tools/vs-2019/docker-container-registry.png)

3. 选择“新建 Azure 容器注册表”。
 
   ![“‘发布’对话框 - 选择‘新建 Azure 容器注册表’”的屏幕截图](media/container-tools/vs-2019/select-existing-or-create-new-azure-container-registry.png)

4. 在“Azure 容器注册表”屏幕中填写所需的值。

    | 设置      | 建议的值  | 描述                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **DNS 前缀** | 全局唯一名称 | 用于唯一标识容器注册表的名称。 |
    | **订阅** | 选择订阅 | 要使用的 Azure 订阅。 |
    | **[资源组](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  要在其中创建容器注册表的资源组的名称。 选择“新建”创建新的资源组。|
    | **[SKU](/azure/container-registry/container-registry-skus)** | 标准 | 容器注册表的服务层  |
    | **注册表位置** | 靠近你的位置 | 在你附近或将使用容器注册表的其他服务附近的[区域](https://azure.microsoft.com/regions/)中，选择位置。 |

    ![Visual Studio 的创建 Azure 容器注册表对话框](media/hosting-web-apps-in-docker/vs-acr-provisioning-dialog-2019.png)

5. 单击 **“创建”** 。

6. 选择“完成”以完成该过程。
::: moniker-end

现在可以将容器从注册表中拖放到任何能够运行 Docker 映像的主机上，例如[Azure 容器实例](/azure/container-instances/container-instances-tutorial-deploy-app)。

## <a name="see-also"></a>另请参阅

[快速入门：使用 Azure CLI 在 Azure 中部署容器实例](/azure/container-instances/container-instances-quickstart)
