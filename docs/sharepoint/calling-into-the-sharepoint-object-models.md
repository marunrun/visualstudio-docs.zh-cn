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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62988399"
---
# <a name="call-into-the-sharepoint-object-models"></a>调入 SharePoint 对象模型
  在 Visual Studio 中创建 SharePoint 工具扩展时，可能需要调用 SharePoint Api 才能执行某些任务。 例如，如果为 SharePoint 项目创建自定义部署步骤，则可能必须调用 SharePoint Api 来执行某些任务来部署解决方案。

 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] 和 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] 提供了两个不同的对象模型，可以在 SharePoint 工具扩展中使用：服务器对象模型和客户端对象模型。 每个对象模型在 SharePoint 工具扩展的上下文中都有优点和缺点。

 有关 SharePoint 对象模型的概述，请参阅 [sharepoint 工具扩展的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)。

## <a name="use-the-client-object-model-in-extension-projects"></a>在扩展项目中使用客户端对象模型
 当你为 SharePoint 工具开发扩展时，可以在项目中使用客户端对象模型，就像任何其他托管 Api。 您可以向您的项目添加对客户端对象模型中的程序集的引用，并且您可以直接从代码中调用客户端对象模型中的 Api。

 但是，在 SharePoint 工具扩展的上下文中，客户端对象模型有两个缺点：

- 客户端对象模型仅提供服务器对象模型的子集。 如果你必须使用客户端对象模型中未公开的 SharePoint 功能，则必须使用服务器对象模型。

- 尽管在大多数情况下，在 SharePoint 工具扩展中使用客户端对象模型，但在某些情况下，客户端对象模型调用无法按预期方式工作。 客户端对象模型设计为在客户端应用程序中用于调用远程服务器或场中的 SharePoint 站点。 Visual Studio 中的 SharePoint 工具仅适用于开发计算机上的本地 SharePoint 安装。 因此，当您在 SharePoint 工具扩展中使用客户端对象模型时，您将调入到本地计算机上的 SharePoint 站点，这并不是客户端对象模型的设计方式。

  有关演示如何在 Visual Studio 中的 SharePoint 工具扩展中使用客户端对象模型的演练，请参阅 [演练：在服务器资源管理器扩展中调入 sharepoint 客户端对象模型](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)。

## <a name="use-the-server-object-model-in-extension-projects"></a>在扩展项目中使用服务器对象模型
 服务器对象模型是客户端对象模型的超集。 使用服务器对象模型时，可以使用 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] 以编程方式公开的所有功能。

 SharePoint 工具扩展可以使用服务器对象模型中的 Api，但不能直接调用 Api。 只能从面向 .NET Framework 3.5 的64位进程调用服务器对象模型。 但是，SharePoint 工具扩展需要， [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 并且它们在32位 Visual Studio 进程中运行。 这可以防止 SharePoint 工具扩展直接引用 SharePoint 服务器对象模型中的程序集。

 如果要在 SharePoint 工具扩展中使用服务器对象模型，则必须创建自定义 *SharePoint 命令* 以调用 API。 在可直接调入服务器对象模型的辅助程序集中定义 SharePoint 命令。 在扩展项目中，使用对象的 ExecuteCommand 方法间接调用 SharePoint 命令 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> 。

 有关创建和使用 SharePoint 命令的详细信息，请参阅 [如何：创建 sharepoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md) 和 [如何：执行 sharepoint 命令](../sharepoint/how-to-execute-a-sharepoint-command.md)。 有关如何部署 SharePoint 命令的信息，请参阅 [在 Visual Studio 中部署 sharepoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

 有关演示如何创建和使用 SharePoint 命令的演练，请参阅 [演练：为 SharePoint 项目创建自定义部署步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md) 和 [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

### <a name="understand-how-sharepoint-commands-are-executed"></a>了解如何执行 SharePoint 命令
 定义 SharePoint 命令的程序集在名为 *vssphost4.exe*的64位主机进程中加载。 在 SharePoint 工具扩展中调用 SharePoint 命令后，命令将由 *vssphost4.exe* 而不是32位 Visual Studio 进程来执行 (*devenv.exe*) 。 您可以通过设置注册表中的值来控制执行 SharePoint 命令的一些方面。 有关详细信息，请参阅 [Visual Studio 中的 SharePoint 工具调试扩展](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [如何：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)
- [如何：执行 SharePoint 命令](../sharepoint/how-to-execute-a-sharepoint-command.md)
- [SharePoint 工具扩展的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
