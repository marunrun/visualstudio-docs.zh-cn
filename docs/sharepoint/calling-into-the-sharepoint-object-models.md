---
title: 调入 SharePoint 对象模型 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, client object model
- SharePoint development in Visual Studio, server object model
- SharePoint commands [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, extensibility features
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 24634143a40f7b163c0b658bddb5596041868033
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62988399"
---
# <a name="call-into-the-sharepoint-object-models"></a>调入 SharePoint 对象模型
  在 Visual Studio 中创建 SharePoint 工具扩展时，可能需要调用 SharePoint Api 来执行特定任务。 例如，如果创建 SharePoint 项目自定义部署步骤时，您可能需要调用 SharePoint Api 来执行一些任务来部署解决方案。

 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] 和[!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)]提供可以在 SharePoint 工具扩展中使用的两个不同的对象模型： 服务器对象模型和客户端对象模型。 每个对象模型在 SharePoint 工具扩展的上下文中具有的优点和缺点。

 SharePoint 对象模型的概述，请参阅[概述的编程模型的 SharePoint 工具扩展](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)。

## <a name="use-the-client-object-model-in-extension-projects"></a>在扩展项目中使用客户端对象模型
 当开发适用于 SharePoint 工具扩展时，您可以像任何其他组托管 Api 在项目中使用客户端对象模型。 可以在客户端对象模型中添加对程序集的引用，到你的项目，并在代码中直接调用在客户端对象模型 Api。

 但是，客户端对象模型在 SharePoint 工具扩展的上下文中有两个缺点：

- 客户端对象模型提供了服务器对象模型的一个子集。 如果必须使用不在客户端对象模型中公开的 SharePoint 功能，则必须使用服务器对象模型。

- 尽管 SharePoint 工具扩展中使用客户端对象模型应运行在大多数情况下，可能会遇到某些情况下，其中对客户端对象模型执行操作无法按预期工作。 客户端对象模型用于在客户端应用程序中用于调入 SharePoint 站点上的远程服务器或场。 Visual Studio 中的 SharePoint 工具只使用在开发计算机上的本地 SharePoint 安装。 因此，在 SharePoint 工具扩展中使用客户端对象模型，可调用到 SharePoint 站点是不如何客户端对象模型专门设计用来在本地计算机上。

  有关演示如何使用客户端对象模型中的 Visual Studio 中的 SharePoint 工具扩展的演练，请参阅[演练：调入 SharePoint 客户端对象模型中的服务器资源管理器扩展](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)。

## <a name="use-the-server-object-model-in-extension-projects"></a>在扩展项目中使用服务器对象模型
 服务器对象模型是客户端对象模型的超集。 当您使用服务器对象模型时，可以使用所有功能，[!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)]和[!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)]以编程方式公开。

 SharePoint 工具扩展可以在服务器对象模型中，使用 Api，但它们不能直接调用 Api。 面向.NET Framework 3.5 可仅从 64 位进程调用服务器对象模型。 但是，SharePoint 工具扩展需要[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]和它们在 32 位 Visual Studio 进程中运行。 这可以防止 SharePoint 工具扩展直接引用 SharePoint 服务器对象模型中的程序集。

 如果你想要在 SharePoint 工具扩展中使用服务器对象模型，则必须创建一个自定义*SharePoint 命令*来调用 API。 在直接调用到服务器对象模型的辅助程序集中定义的 SharePoint 命令。 在扩展项目中，您的 SharePoint 命令间接使用调用的 ExecuteCommand 方法<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection>对象。

 有关创建和使用 SharePoint 命令的详细信息，请参阅[如何：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)和[如何：执行 SharePoint 命令](../sharepoint/how-to-execute-a-sharepoint-command.md)。 有关如何部署 SharePoint 命令的信息，请参阅[部署的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

 有关演示如何创建和使用 SharePoint 命令的演练，请参阅[演练：创建 SharePoint 项目的自定义部署步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)和[演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

### <a name="understand-how-sharepoint-commands-are-executed"></a>了解如何执行 SharePoint 命令
 定义 SharePoint 命令的程序集是在名为的 64 位主机进程中加载*vssphost4.exe*。 在 SharePoint 工具扩展中调用 SharePoint 命令后，该命令将执行通过*vssphost4.exe*而不是 32 位 Visual Studio 进程 (*devenv.exe*)。 您可以控制在注册表中设置的值执行 SharePoint 命令的某些方面。 有关详细信息，请参阅[调试的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [如何：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)
- [如何：执行 SharePoint 命令](../sharepoint/how-to-execute-a-sharepoint-command.md)
- [工具扩展的 SharePoint 的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
