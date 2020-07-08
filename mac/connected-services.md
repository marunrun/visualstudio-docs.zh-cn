---
title: 连接的服务
description: 在 Visual Studio for Mac 中将 Azure 数据存储、身份验证和推送通知添加到移动应用
ms.assetid: 41CB62FF-0F39-4CE8-8917-6A77F058719F
author: sayedihashimi
ms.author: sayedha
ms.date: 11/06/2018
ms.topic: how-to
ms.openlocfilehash: 8a1287d82096677d20a498756de3d2a9f5af259b
ms.sourcegitcommit: 2ce59c2ffeba5ba7f628c2e6c75cba4731deef8a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2020
ms.locfileid: "85938766"
---
# <a name="connected-services-walkthrough"></a>“连接的服务”演练

连接的服务工作流将 Azure 门户工作流引入到 Visual Studio for Mac，因此不必离开项目即可添加服务。

此演练介绍如何添加 Azure 后端服务，该服务将云数据存储、身份验证和推送通知引入到跨平台 Xamarin.Forms 可移植类库 (PCL) 应用程序。

1. 首先双击解决方案中的“连接服务”节点，随即出现“服务库”   。
  这是一个列表，其中列出了适用于该应用程序类型的所有可用服务。 通过单击选择服务（例如“Azure App Service 的移动后端”）  。

    [![Visual Studio for Mac 中连接的服务节点](media/connected-services-image001-sml.png "Visual Studio for Mac 中连接的服务节点")](media/connected-services-image001.png#lightbox)

2. 服务详细信息页面包含服务描述和要安装的依赖项。
  单击“添加”按钮，将依赖项添加到应用  ：

    [![使用 Azure 的移动后端](media/connected-services-image002-sml.png "使用 Azure 的移动后端")](media/connected-services-image002.png#lightbox)

3. 依赖项需要添加到 PCL 和特定于平台的项目才能工作。
  选择复选框，将服务添加到会（直接或间接）引用它的每个项目：

    [![检查应引用此服务的所有项目](media/connected-services-image003-sml.png "检查应引用此服务的所有项目")](media/connected-services-image003.png#lightbox)

4. 在 NuGet 包的“许可证接受”对话框上选择“接受”   。
  可能需要接受两个对话框：一个用于 MobileClient 和依赖项，另一个用于 SQLiteStore，这是脱机数据同步所必需的：

    [![接受许可协议](media/connected-services-image004-sml.png "接受许可协议")](media/connected-services-image004.png#lightbox)

    ![“许可证接受”窗口](media/connected-services-image005.png "“许可证接受”窗口")

5. 添加依赖项后，系统将要求使用你想要用来与 Azure 通信的帐户登录。
  如果已使用 Microsoft ID 登录，则 Visual Studio for Mac 将尝试提取 Azure 订阅以及与其相关的任何应用服务。 如果没有订阅，则可以通过注册免费试用版或在 Azure 门户中购买订阅计划来添加订阅。

6. 从列表中选择应用服务。 这将使用 Azure 应用服务的相应 URL 填充 `MobileServiceClient` 对象的模板代码：

    [![从列表中选择应用服务](media/connected-services-image006-sml.png "从列表中选择应用服务")](media/connected-services-image006.png#lightbox)

    如果没有列出服务，请单击“新建”按钮（参阅步骤 9） 

7. 将 `MobileServiceClient` 的模板代码复制到 PCL。 文件位置并不重要，只要只有这一个实例即可。
  建议的方法是创建一个 `AzureService` 类，用于处理所有 Azure 交互并使用 `MobileServiceClient`：

    ![将配置代码复制到应用](media/connected-services-image007.png "将配置代码复制到应用")

8. 按照“后续步骤”中的文档说明，将数据、脱机同步、身份验证和推送通知添加到应用  ：

    [![查看后续步骤说明](media/connected-services-image008-sml.png "查看后续步骤说明")](media/connected-services-image008.png#lightbox)

9. 如果没有现有应用服务，可以在 Visual Studio for Mac 中创建新的服务。
  单击服务列表左下角的“新建”按钮，打开“新建应用服务”对话框   ：

    [![在 Visual Studio for Mac 中创建新的应用服务](media/connected-services-image009-sml.png "在 Visual Studio for Mac 中创建新的应用服务")](media/connected-services-image009.png#lightbox)

新服务需要下列参数：

- **应用服务名称** – 计划的唯一名称/ID
- **订阅** – 想要用于支付该服务的订阅
- **资源组** – 一种为项目组织所有 Azure 资源的方法。 可以选择使用现有资源组，也可以创建新的。 如果是第一个 Azure 服务，请创建一个新资源组。
- **服务计划** – 确定使用计划的任何资源的位置和成本。 可以选择使用现有资源组，也可以创建新的。 如果是第一个 Azure 服务，请使用默认服务计划或在免费层 (F1) 中创建新的。

访问[移动应用文档](/azure/app-service-mobile/)，获取详细信息。

## <a name="see-also"></a>另请参阅

- [连接服务（Windows 上的 Visual Studio）](/visualstudio/azure/vs-azure-tools-connected-services-storage)