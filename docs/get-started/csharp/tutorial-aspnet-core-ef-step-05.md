---
title: 步骤 5：将 ASP.NET Core 应用部署到 Azure
description: 通过本视频教程和分步说明将 ASP.NET Core Web 应用部署到 Azure。
ms.custom: get-started
ms.date: 08/14/2020
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
monikerRange: vs-2019
ms.topic: tutorial
ms.devlang: CSharp
author: ardalis
ms.author: ornella
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: 55dd48ed2c319984fcc96e806c97a7ae24ce7170
ms.sourcegitcommit: 577c905de52057a741e68c2ed168ea527813fda5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88248714"
---
# <a name="step-5-deploy-your-aspnet-core-app-to-azure"></a>步骤 5：将 ASP.NET Core 应用部署到 Azure

请按照下列步骤将 ASP.NET Core 应用及其数据库部署到 Azure。

观看此视频，按照说明向 Azure 部署首个 ASP.NET Core 应用。 

> [!VIDEO https://www.youtube.com/embed/n8wz_f5_4wI]

## <a name="open-your-project"></a>打开项目

在 Visual Studio 2019 中打开 ASP.NET Core 应用。 该应用应已使用 EF Core 和有效的 Web API 进行设置，如[本系列教程步骤 4](tutorial-aspnet-core-ef-step-04.md) 中所配置的那样。

## <a name="publish-to-azure-app-service"></a>发布到 Azure 应用服务

1. 在“解决方案资源管理器”中右键单击该项目，然后选择“发布”  。 在“发布”向导中，选择“Azure”作为目标 。

   ![Azure 应用服务 1 的屏幕截图](media/vs-2019/app-service-screen-1.png)

1. 对于特定目标，请选择“Azure 应用服务(Windows)”。

   ![Azure 应用服务 2 的屏幕截图](media/vs-2019/app-service-screen-2.png)

1. 选择“新建 Azure 应用服务”。 如果还没有 Azure 帐户，请单击“创建免费 Azure 帐户”**** 并完成简短的注册过程。

   ![Azure 应用服务 3 的屏幕截图](media/vs-2019/app-service-screen-3.png)

1. 指定名称和资源组，或接受默认值，然后选择“创建”。 资源组只是在 Azure 中组织相关资源（例如与存储帐户、密钥保管库和数据库协同工作的服务）的一种方式。

   ![Azure 应用服务 4 的屏幕截图](media/vs-2019/app-service-screen-4.png)

1. 选择“完成”。 在 Azure 中创建资源，部署应用，并使用刚创建的内容的相关信息填充“发布”选项卡。 “发布”选项卡提供了一个按钮，只需单击一下即可发布相同的配置，并且显示了配置详细信息，或使你可以添加数据库等服务。

现在，请添加 Azure SQL Server 数据库。

1. 在“发布”选项卡的“服务依赖项”下的“SQL Server 数据库”旁边，选择“配置”   。

1. 在下一个屏幕上，选择“Azure SQL 数据库”。

   ![“Azure SQL 数据库”屏幕的屏幕截图](media/vs-2019/app-service-azure-sql-db.png)

1. 在“配置 SQL 数据库”屏幕上，选择“创建 SQL 数据库” 。

   ![“配置 SQL 数据库”屏幕的屏幕截图](media/vs-2019/app-service-azure-sql-db-2.png)

1. 在“Azure SQL 数据库:新建”屏幕上，创建新的数据库服务器。

   ![屏幕截图“Azure SQL 数据库:创建新的](media/vs-2019/app-service-azure-sql-db-3.png)

1. 在“SQL Server:新建”屏幕上，选择名称和位置，并指定管理员用户名和密码。

   ![Visual Studio 2019 创建 Azure SQL Server](media/vs-2019/app-service-azure-sql-db-overlayed.png)

## <a name="exploring-the-azure-portal-and-your-hosted-app"></a>浏览 Azure 门户和托管应用

创建应用服务后，将在浏览器中启动网站。 加载网站时，还可以在 Azure 门户中找到应用服务。 浏览应用服务的可用选项，将会发现可在其中启动和停止应用的“概述”**** 部分。

![Azure 应用服务选项](media/vs-2019/vs2019-azure-app-service-menu-options.png)

### <a name="scalability"></a>可伸缩性

可以查看纵向扩展以及横向扩展应用的选项。纵向扩展是指增加为托管应用的每个实例提供的资源。 横向扩展是指增加托管应用的实例数。 可以为应用配置自动缩放，它将自动增加用于托管应用的实例数以响应负载，然后在负载减少后减少实例数。

### <a name="security-and-compliance"></a>安全性与符合性

使用 Azure 托管应用的另一个好处是安全性和合规性。 Azure 应用服务提供 ISO、SOC 和 PCI 符合性。 我们可以选择通过 Azure Active Directory 或 Twitter、Facebook、Google 或 Microsoft 等社交登录对用户进行身份验证。 可以创建 IP 限制、管理服务标识、添加自定义域、支持应用的 SSL，以及使用应用的内容、配置和数据库的可恢复存档副本配置备份。 这些功能可通过“身份验证/授权”、“标识”、“备份”和“SSL 设置”菜单选项访问。

### <a name="deployment-slots"></a>部署槽

通常在部署应用时，在应用重启期间会有一小段停机时间。 部署槽位允许你部署到一个单独的暂存实例或一组实例，并在将它们交换到生产环境之前对其进行预热，从而避免了这个问题。 交换只是即时无缝的流量重定向。 如果在交换后的生产中出现任何问题，始终可以切换回最后一个已知良好的生产状态。

## <a name="update-connection-string"></a>更新连接字符串

默认情况下，Azure 希望新应用连接到其新的 SQL Server 数据库，以使用名为 `DefaultConnection` 的连接字符串。 目前，我们在本系列教程的前面创建的应用使用名为 `AppDbContext` 的连接字符串。 需要在 appsettings.json** 和 Startup.cs** 中对此进行更改，然后重新部署应用。

## <a name="test-the-app-running-in-azure"></a>测试在 Azure 中运行的应用

导航到 /Games** 路径，应能够添加一个新游戏并看到它显示在其中。 接下来，导航到 /swagger** 路径，应能够使用其中的 Web API 终结点确认应用的 API 也工作正常。

恭喜！ 你已经完成本系列视频教程！

## <a name="next-steps"></a>后续步骤

了解关于如何使用这些免费资源构建 ASP.NET Core 应用程序的详细信息。

[ASP.NET Core 应用程序体系结构](https://dotnet.microsoft.com/learn/web/aspnet-architecture)

## <a name="see-also"></a>另请参阅

- [使用 Visual Studio 将 ASP.NET Core 应用发布到 Azure](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs?view=aspnetcore-2.2)