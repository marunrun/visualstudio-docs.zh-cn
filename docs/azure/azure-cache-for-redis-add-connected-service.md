---
title: 使用连接的服务添加适用于 Redis 的 Azure 缓存 |Microsoft Docs
description: 使用 Visual Studio 添加连接的服务，将用于 Redis 支持的 Azure 缓存添加到应用
author: AngelosP
manager: jillfra
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 08/17/2020
ms.author: angelpe
monikerRange: '>= vs-2019'
ms.openlocfilehash: 7583848c4bbe38f9094c60998e16ca3e95cf399f
ms.sourcegitcommit: 3ef987e99616c3eecf4731bf5ac89e16238e68aa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88643115"
---
# <a name="add-azure-cache-for-redis-by-using-visual-studio-connected-services"></a>使用 Visual Studio 连接的服务添加适用于 Redis 的 Azure 缓存

使用 Visual Studio，可以使用 **连接的服务** 功能将以下任意内容连接到用于 Redis 的 Azure 缓存：

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

## <a name="connect-to-azure-cache-for-redis-using-connected-services"></a>使用连接的服务连接到用于 Redis 的 Azure 缓存

1. 在 Visual Studio 中打开项目。

1. 在 **解决方案资源管理器**中，右键单击 " **连接的服务** " 节点，然后从上下文菜单中选择 " **添加连接的服务**"。

1. 在 " **连接的服务** " 选项卡中，选择 " **服务依赖项**的 + 图标"。

    ![添加服务依赖项](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. 在 " **添加依赖关系** " 页上，选择 " **Azure Cache for Redis**"。

    ![为 Redis 添加 Azure 缓存](./media/azure-redis-cache-add-connected-service/azure-redis-cache.png)

    如果尚未登录，请登录到 Azure 帐户。 如果没有 Azure 帐户，可以注册[免费试用版](https://azure.microsoft.com/account/free)。

1. 在 " **为 Redis 配置 Azure 缓存** " 屏幕中，为 Redis 选择现有的 azure 缓存，然后选择 " **下一步**"。

    如果需要创建新的组件，请参阅下一步。 否则，请跳到步骤 7。

    ![连接到 Redis 的现有 Azure 缓存](./media/azure-redis-cache-add-connected-service/created-azure-redis-cache.png)

1. 若要创建 Azure Redis 缓存：

   1. 选择屏幕底部的 " **创建新的 Azure Redis 缓存** "。

   1. 填写 Redis 的 **Azure 缓存：创建新** 屏幕，然后选择 " **创建**"。

       ![适用于 Redis 的新 Azure 缓存](./media/azure-redis-cache-add-connected-service/create-new-azure-redis-cache.png)

   1. 当显示 " **配置 Azure Cache For Redis** " 屏幕时，新缓存将显示在列表中。 在列表中选择新数据库，然后选择 " **下一步**"。

1. 输入连接字符串名称，或选择默认值，并选择是要将连接字符串存储在本地机密文件中还是 [Azure Key Vault](/azure/key-vault)中。

   ![指定连接字符串](./media/azure-redis-cache-add-connected-service/connection-string.png)

1. " **更改摘要** " 屏幕显示了在完成该过程后，将对项目进行的所有修改。 如果更改看起来正常，请选择 " **完成**"。

   ![更改摘要](./media/azure-redis-cache-add-connected-service/summary-of-changes.png)

1. 该连接将显示在 "**连接的服务**" 选项卡的 "**服务依赖项**" 部分下。

   ![服务依赖项](./media/azure-redis-cache-add-connected-service/service-dependencies-after.png)

## <a name="see-also"></a>另请参阅

- [Azure Cache for Redis 产品页](https://azure.microsoft.com/services/cache)
- [适用于 Redis 的 Azure 缓存文档](/azure/azure-cache-for-redis/)
- [连接服务 (Visual Studio for Mac)](/visualstudio/mac/connected-services)