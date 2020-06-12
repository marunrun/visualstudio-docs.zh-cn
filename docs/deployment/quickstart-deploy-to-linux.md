---
title: 发布到 Linux 上的应用服务
ms.date: 01/29/2019
ms.topic: quickstart
helpviewer_keywords:
- deployment, website
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- azure
ms.openlocfilehash: 1a6500b8b38cc6beef21e7da301ec8e1ef7d4bd6
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84173219"
---
# <a name="publish-an-aspnet-core-app-to-app-service-on-linux-using-visual-studio"></a>使用 Visual Studio 将 ASP.NET Core 应用发布到 Linux 上的应用服务

从 Visual Studio 2017 版本 15.7 开始，可以使用以下任一方法将 ASP.NET Core 应用发布到 Azure 应用服务 Linux（使用容器）。

* 对于应用的连续（或自动）部署，请将 Azure DevOps 与 [Azure 管道](https://docs.microsoft.com/azure/devops/pipelines/get-started-yaml?view=azdevops)结合使用。

* 对于应用的一次性（或手动）部署，请使用 Visual Studio 中的“Publish”工具将 ASP.NET Core 应用部署到适用于 Linux 的应用服务（使用容器）。

本文介绍如何使用“Publish”工具进行一次性部署。

[!INCLUDE [quickstart-prereqs-azure-linux](includes/quickstart-prereqs-azure-linux.md)]

## <a name="publish-to-azure-app-service-on-linux"></a>发布到 Linux 上的 Azure 应用服务

1. 在解决方案资源管理器中，右键单击该项目并选择“发布”（或使用“生成” > “发布”菜单项）  。

    ![解决方案资源管理器中项目上下文菜单上的“发布”命令](../deployment/media/quickstart-publish.png "选择发布")

1. 在“发布”对话框中，选择 Azure 。

    ![选择发布目标](../deployment/media/quickstart-publish-azure.png)

1. 选择“Azure 应用服务(Linux)”，然后选择“下一步” 。

    ![选择“Linux 上的 Azure 应用服务”](../deployment/media/quickstart-publish-linux-select-azure-service.png)

1. 如有必要，请用 Azure 帐户登录。 选择“创建新的 Azure 应用服务…”

    ![用于创建新的 Azure 应用服务实例的链接](../deployment/media/quickstart-publish-linux-create-new-link.png)

1. 在“创建 Azure 应用服务(Linux)”对话框中，填写“应用名称”、“资源组”和“应用服务计划”输入字段   。 可以保留这些名称，也可以进行更改。 准备就绪后，选择“创建”。

    ![选择 Azure 应用服务](../deployment/media/quickstart-publish-linux-create-new-dialog.png)

1. 在“发布”对话框中，将自动选择新创建的实例。 准备就绪后，单击“完成”。

    ![选择 Azure 应用服务](../deployment/media/quickstart-publish-linux-select-instance.png)

1. 选择“发布”。 Visual Studio 将应用部署到 Azure 应用服务，并且 Web 应用将在浏览器中加载。 项目属性“发布”窗格显示了站点 URL 和其他详细信息。

    ![显示配置文件摘要的“发布”属性窗格](../deployment/media/quickstart-publish-linux-summary-page.png)

## <a name="clean-up-resources"></a>清理资源

在前面步骤中，已在资源组中创建 Azure 资源。 如果以后不需要这些资源，可以通过删除资源组来删除它们。
从 Azure 门户左侧菜单中，选择“资源组”，然后选择“myResourceGroup” 。
在资源组页上，确保列出的资源是要删除的。
选择“删除”，在文本框中键入“myResourceGroup”，然后选择“删除”  。

## <a name="next-steps"></a>后续步骤

在本快速入门中，了解如何使用 Visual Studio 创建发布配置文件，以便将其部署到 Linux 上的应用服务。 建议阅读有关使用 Azure 发布到 Linux 的更多信息。

> [!div class="nextstepaction"]
> [Linux 应用服务](/azure/app-service/containers/app-service-linux-intro)
