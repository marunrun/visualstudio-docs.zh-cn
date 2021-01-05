---
title: 使用连接的服务添加 Azure 应用配置 |Microsoft Docs
description: 使用 Visual Studio 连接的服务向应用添加 Azure 配置服务依赖项
author: ghogen
manager: ''
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 12/11/2020
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: a0db2f2e4993fcc3c986686322b8915615758e13
ms.sourcegitcommit: fcfd0fc7702a47c81832ea97cf721cca5173e930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2020
ms.locfileid: "97727289"
---
# <a name="adding-azure-app-configuration-by-using-visual-studio-connected-services"></a>使用 Visual Studio 连接的服务添加 Azure 应用配置

在本教程中，你将了解如何在使用 ASP.NET Core 或任何类型的 ASP.NET 项目时，在 Visual Studio 中轻松添加开始使用 Azure 应用配置来管理你的 web 项目的配置和功能标志所需的所有内容。 通过使用 Visual Studio 中的连接的服务功能，可以让 Visual Studio 自动添加连接到 Azure 中的应用配置资源所需的所有代码、NuGet 包和配置设置。 若要使用此功能，必须使用 Visual Studio 2019 版本16.9 或更高版本。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 有关 Visual Studio for Mac，请参阅 [Visual Studio for Mac 中连接服务](/visualstudio/mac/connected-services)。

## <a name="prerequisites"></a>先决条件

- 已安装 Azure 工作负荷的 Visual Studio。
- 受支持类型之一的项目

## <a name="connect-to-azure-app-configuration-using-connected-services"></a>使用连接的服务连接到 Azure 应用配置

1. 在 Visual Studio 中打开项目。

1. 在 **解决方案资源管理器** 中，右键单击 " **连接的服务** " 节点，然后从上下文菜单中选择 " **添加连接的服务**"。

    ![添加 Azure 连接服务](./media/vs-azure-tools-connected-services-storage/vs-2019/add-connected-service.png)

1. 在 " **连接的服务** " 选项卡中，选择 " **服务依赖项** 的 + 图标"。

    ![添加服务依赖项](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. 在 " **添加依赖关系** " 页上，选择 " **Azure 应用配置**"。

    ![添加应用配置](./media/vs-azure-tools-connected-services-app-configuration/add-azure-app-configuration.png)

    如果尚未登录，请登录到 Azure 帐户。 如果没有 Azure 帐户，可以注册[免费试用版](https://azure.microsoft.com/free/dotnet)。

1. 在 " **配置 Azure 应用配置** " 屏幕上，选择你的订阅和现有的配置存储。 然后，选择“下一步”。

    如果需要创建应用配置存储，请参阅下一步。 否则，请跳到步骤 6。

    ![向项目添加现有配置帐户](./media/vs-azure-tools-connected-services-app-configuration/select-config-store.png)

1. 创建应用配置存储区：

   1. 选择 " **应用配置存储** " 标头右侧的 "+" 图标。 

   1. 填写 " **Azure 应用配置：创建新** 对话框，然后选择" **创建**"。 请注意，"资源名称" 字段必须是唯一的。 

       ![新 Azure 应用配置存储](./media/vs-azure-tools-connected-services-app-configuration/create-new-config-store.png)

   1. 显示 " **Azure 应用配置** " 对话框时，新的配置存储将显示在列表中。 选择此新存储，然后选择 " **下一步**"。

1. 输入连接字符串名称，并选择是要将连接字符串存储在本地机密文件中还是 [Azure Key Vault](/azure/key-vault)中。

   ![指定连接字符串](./media/vs-azure-tools-connected-services-app-configuration/connection-string-app-config.png)

1. " **更改摘要** " 屏幕显示了在完成该过程后，将对项目进行的所有修改。 如果更改看起来正常，请选择 " **完成**"。

   ![更改摘要](./media/vs-azure-tools-connected-services-app-configuration/summary-of-changes-app-config.png)

1. 完成 **依赖项配置过程** 后，Azure 应用配置现在会显示在项目的 " **服务依赖项** " 节点下。

## <a name="next-steps"></a>后续步骤

了解 [Azure 应用配置文档](/azure/azure-app-configuration/overview)中的 Azure 应用配置。

## <a name="see-also"></a>另请参阅

- [在连接 ASP.NET Core 应用的应用配置中使用动态配置的教程](/azure/azure-app-configuration/enable-dynamic-configuration-aspnet-core)
- [连接服务 (Visual Studio for Mac)](/visualstudio/mac/connected-services)