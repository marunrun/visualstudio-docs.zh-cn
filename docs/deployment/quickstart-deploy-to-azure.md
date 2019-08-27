---
title: 发布到 Azure 应用服务
ms.date: 01/29/2019
ms.topic: quickstart
helpviewer_keywords:
- deployment, website
ms.assetid: fc82b1f1-d342-4b82-9a44-590479f0a895
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- azure
ms.openlocfilehash: d1703fb5386c7b29446b621d2e83f9486e93dd3d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65679267"
---
# <a name="publish-a-web-app-to-azure-app-service-using-visual-studio"></a>使用 Visual Studio 将 Web 应用发布到 Azure 应用服务

对于 ASP.NET、ASP.NET Core、Node.js 和 .NET Core 应用，请使用以下任一方法发布到 Azure 应用服务或 Azure 应用服务 Linux（使用容器）。

* 对于应用的连续（或自动）部署，请将 Azure DevOps 与 [Azure 管道](https://docs.microsoft.com/azure/devops/pipelines/get-started-yaml?view=azdevops)结合使用。

* 对于应用的一次性（或手动）部署，请使用 Visual Studio 中的“Publish”工具将 ASP.NET、ASP.NET Core、Node.js 和 .NET Core 应用部署到 Azure 应用服务或适用于 Linux 的应用服务（使用容器）  。 对于 Python 应用，请按照 [Python - 发布到 Azure 应用服务](../python/publishing-python-web-applications-to-azure-from-visual-studio.md)上的步骤操作。

本文介绍如何使用“Publish”工具进行一次性部署  。

[!INCLUDE [quickstart-prereqs-azure](includes/quickstart-prereqs-azure.md)]

## <a name="publish-to-azure-app-service"></a>发布到 Azure 应用服务

1. 在解决方案资源管理器中，右键单击该项目并选择“发布”（或使用“生成” > “发布”菜单项）    。

    ![解决方案资源管理器中项目上下文菜单上的“发布”命令](../deployment/media/quickstart-publish.png "选择“发布”")

1. 如果之前配置了任何发布配置文件，则会显示“发布”窗格，在这种情况下，请选择“新建配置文件”   。

1. 在“选取发布目标”对话框中，选择“应用服务”   。

    ![选择 Azure 应用服务](../deployment/media/quickstart-publish-azure.png "Choose Azure App Service")

1. 选择“发布”  。 “创建应用服务”对话框随即显示  。 使用 Azure 帐户登录，如果有必要，默认应用服务设置将填充字段。

    ![创建应用服务](../deployment/media/quickstart-publish-settings-app-service.png "Create Azure App Service")

1. 选择“创建”  。 Visual Studio 将应用部署到 Azure 应用服务，并且 Web 应用将在浏览器中加载。 项目属性“发布”窗格显示了站点 URL 和其他详细信息  。

    ![显示配置文件摘要的“发布”属性窗格](../deployment/media/quickstart-publish-app-service-summary.png)

## <a name="clean-up-resources"></a>清理资源

在前面步骤中，已在资源组中创建 Azure 资源。 如果以后不需要这些资源，可以通过删除资源组来删除它们。
从 Azure 门户左侧菜单中，选择“资源组”，然后选择“myResourceGroup”   。
在资源组页上，确保列出的资源是要删除的。
选择“删除”，在文本框中键入“myResourceGroup”，然后选择“删除”    。

## <a name="next-steps"></a>后续步骤

在本快速入门中，学习了如何使用 Visual Studio 创建用于部署到 Azure 的发布配置文件。 还可以通过从 Azure 应用服务导入发布设置来配置发布配置文件。

> [!div class="nextstepaction"]
> [导入发布设置并部署到 Azure](tutorial-import-publish-settings-azure.md)
