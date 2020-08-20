---
title: 使用连接的服务添加 Azure SignalR |Microsoft Docs
description: 使用 Visual Studio 添加连接的服务，将 Azure SignalR 添加到应用
author: AngelosP
manager: jillfra
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 08/17/2020
ms.author: angelpe
monikerRange: '>= vs-2019'
ms.openlocfilehash: 0e44416bd6a55796b62a7590856caab8466a6401
ms.sourcegitcommit: 3ef987e99616c3eecf4731bf5ac89e16238e68aa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88643106"
---
# <a name="add-azure-signalr-by-using-visual-studio-connected-services"></a>使用 Visual Studio 连接的服务添加 Azure SignalR

使用 Visual Studio，可以使用 **连接的服务** 功能将以下任何内容连接到 Azure SignalR 服务：

- .NET Framework 控制台应用
- ASP.NET MVC ( .NET Framework)  
- ASP.NET Core
- .NET Core (包括控制台应用程序、WPF、Windows 窗体、类库) 
- .NET Core 辅助角色
- Azure Functions
- 通用 Windows 平台应用
- Xamarin
- Cordova

连接服务功能可将所有需要的引用和连接代码添加到项目，并相应地修改配置文件。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 有关 Visual Studio for Mac，请参阅 [Visual Studio for Mac 中连接服务](/visualstudio/mac/connected-services)。
## <a name="prerequisites"></a>先决条件

- 已安装 Azure 工作负荷的 Visual Studio。
- 受支持类型之一的项目

## <a name="connect-to-azure-signalr-using-connected-services"></a>使用连接的服务连接到 Azure SignalR

1. 在 Visual Studio 中打开项目。

1. 在 **解决方案资源管理器**中，右键单击 " **连接的服务** " 节点，然后从上下文菜单中选择 " **添加连接的服务**"。

1. 在 " **连接的服务** " 选项卡中，选择 " **服务依赖项**的 + 图标"。

    ![添加服务依赖项](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. 在 " **添加依赖关系** " 页上，选择 " **Azure SignalR 服务**"。

    ![添加 Azure SignalR 服务](./media/azure-signalr-add-connected-service/add-signalr-service.png)

    如果尚未登录，请登录到 Azure 帐户。 如果没有 Azure 帐户，可以注册[免费试用版](https://azure.microsoft.com/account/free)。

1. 在 " **配置 Azure SignalR** " 屏幕中，选择现有的 azure SignalR 组件，然后选择 " **下一步**"。

    如果需要创建新的组件，请参阅下一步。 否则，请跳到步骤 7。

    ![连接到现有的 Azure SignalR 组件](./media/azure-signalr-add-connected-service/created-signalr.png)

1. 若要创建 Azure SignalR 服务实例：

   1. 选择屏幕底部的 " **创建新的 Azure SignalR 服务实例** "。

   1. 填写 **Azure SignalR 服务：创建新** 屏幕，然后选择 " **创建**"。

       ![新的 Azure SignalR 服务实例](./media/azure-signalr-add-connected-service/create-new-signalr.png)

   1. 当显示 " **配置 Azure SignalR 服务** " 屏幕时，新实例将出现在列表中。 选择列表中的新实例，然后选择 " **下一步**"。

1. 输入连接字符串名称，或选择默认值，并选择是要将连接字符串存储在本地机密文件中还是 [Azure Key Vault](/azure/key-vault)中。

   ![指定连接字符串](./media/azure-signalr-add-connected-service/connection-string.png)

1. " **更改摘要** " 屏幕显示了在完成该过程后，将对项目进行的所有修改。 如果更改看起来正常，请选择 " **完成**"。

   ![更改摘要](./media/azure-signalr-add-connected-service/summary-of-changes.png)

1. 该连接将显示在 "**连接的服务**" 选项卡的 "**服务依赖项**" 部分下。

   ![服务依赖项](./media/azure-signalr-add-connected-service/service-dependencies-after.png)

## <a name="see-also"></a>另请参阅

- [Azure SignalR 产品页](https://azure.microsoft.com/services/signalr-service/)
- [Azure SignalR 服务文档](/azure/azure-signalr)
- [连接服务 (Visual Studio for Mac)](/visualstudio/mac/connected-services)
