---
title: 发布到 Azure 应用服务
ms.date: 04/02/2019
helpviewer_keywords:
- deployment, website
ms.assetid: 8524a4c5-97a9-41ac-a2a0-034efb9bfc57
author: sayedihashimi
ms.author: sayedha
manager: unniravindranathan
ms.prod: visual-studio-mac
ms.custom: video
ms.workload:
- azure
ms.openlocfilehash: e4ce4273b72a57a2b9456974a108809dcd73b4e0
ms.sourcegitcommit: fe212f8960d7882a1b0fdae9e22f008996aacf3c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2019
ms.locfileid: "70222735"
---
# <a name="publish-a-web-app-to-azure-app-service-using-visual-studio-for-mac"></a>使用 Visual Studio for Mac 将 Web 应用发布到 Azure 应用服务

可使用“发布”工具将 ASP.NET Core 应用发布到 Azure 应用服务。

## <a name="prerequisites"></a>系统必备

- 已安装 [Visual Studio 2019 for Mac](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs4mac2019)，并启用了 ASP.NET Core。
- 一个 Azure 订阅。 如果还没有订阅，请[免费注册](https://azure.microsoft.com/free/dotnet/)，其中包括为期 30 天的 $200 额度和为期 12 个月的热门免费服务。
- ASP.NET Core 项目。 如果还没有项目，则可以[创建一个新的项目](~/create-new-projects.md)。

## <a name="publish-to-azure-app-service"></a>发布到 Azure 应用服务

 1. 在 Solution Pad 中，右键单击项目，选择“发布”  。

    ![“发布”上下文菜单](media/publish-context-menu.png)

 2. 如果之前已将此项目发布到 Azure 应用服务，则在菜单中将看到发布配置文件。 选择该发布配置文件以启动发布过程。

 3. 若要首次将此项目发布到应用服务，请选择“发布到 Azure” 

    ![“发布到应用服务”上下文菜单](media/publish-to-azure-context-menu.png)

 4. “发布到 Azure 应用服务”对话框出现，并且显示任何现有的应用服务  。 若要发布到现有应用服务，请选择列表中的应用服务，然后单击“发布”  。

    ![“发布到 Azure 应用服务”对话框](media/publish-to-app-service-dialog.png)

 5. 若要创建新的应用服务，请单击“新建”按钮  。

    ![“发布到应用服务”对话框](media/publish-to-app-service-dialog-new-selected.png)

 6. “新建应用服务”对话框出现  在此对话框中可以为新的应用服务配置设置。

    ![“新建应用服务”对话框](media/publish-new-app-service.png)

    在此处自定义时需要考虑几个选项。 应用服务的名称将默认为项目名称。 如果名称不可用，则输入字段右侧将显示警告符号。 网站的 URL 中将使用应用服务的名称，因此该名称必须可有效用于 URL。

    可以使用“订阅”下拉列表更改应用服务将与之关联的订阅  。

    可以使用下拉列表选择一个现有资源组，也可以使用 + 按钮创建一个新的资源组   。

    对于应用服务计划，请选择一个现有资源组，或通过选择“自定义”单选按钮创建一个新的资源组  。

    若要创建新的应用服务并向其发布项目，请单击“创建”  。

    单击“创建”后将关闭“新建应用服务”对话框，你应该会看到以下消息，指示创建应用服务已启动   。

      ![创建应用服务消息](media/publish-create-app-service-message.png)

    单击“确定”后将关闭该消息，你可以继续处理项目  。 你可以通过 IDE 顶部的状态栏查看发布过程的状态。 你的 Web 应用成功发布后，站点就会在默认浏览器中打开。

## <a name="related-video"></a>相关视频

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Publish-to-Azure/player]
