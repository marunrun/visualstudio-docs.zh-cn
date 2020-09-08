---
title: 在 Visual Studio 中扩展 SharePoint 工具 | Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Studio, extending tools
- extensibility [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, extending tools
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7dc0cc0d0af73d032d870629877b62c94e6b347b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86016040"
---
# <a name="extend-the-sharepoint-tools-in-visual-studio"></a>在 Visual Studio 中扩展 SharePoint 工具
  Visual Studio 中的 SharePoint 工具可满足许多应用程序开发方案的要求。 但是，你可能会发现存在它们未提供你或其他开发人员所需的功能的情况。 在这些情况下，可以扩展 SharePoint 工具以创建所需的功能。

## <a name="how-to-extend-the-sharepoint-tools"></a>如何扩展 SharePoint 工具
 可以在“服务器资源管理器”窗口中扩展 SharePoint 项目系统和“SharePoint 连接”节点 。

### <a name="extend-the-sharepoint-project-system"></a>扩展 SharePoint 项目系统
 Visual Studio 包含一组可用于创建 SharePoint 解决方案的项目模板和项模板。 例如，用于事件接收器、列表定义、工作流和 Web 部件的模板。 但是，你也可以定义自己的 SharePoint 项目项类型，用于创建 SharePoint 组件，如字段或自定义操作。 还可以为 Visual Studio 中已安装的 SharePoint 项目项类型创建扩展，以及为 SharePoint 项目创建扩展。

 有关详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

### <a name="extend-the-sharepoint-connections-node-in-server-explorer"></a>扩展服务器资源管理器中的“SharePoint 连接”节点
 在 Visual Studio 中，可以使用“服务器资源管理器”窗口中的“SharePoint 连接”节点，在分层树状视图中查看一个或多个本地 SharePoint 站点的许多组件 。 还可以通过以下方式扩展“SharePoint 连接”节点：

- 通过添加你自己的节点。 如果想要显示默认情况下不显示的 SharePoint 站点组件，这将很有用。

- 通过扩展现有节点。 例如，可以将新的子节点添加到现有节点，或者可以将快捷菜单项添加到节点，并在开发人员单击菜单项时执行任务。

  有关详细信息，请参阅[扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

## <a name="development-computer-requirements"></a>开发计算机要求
 要为 SharePoint 工具创建扩展，开发计算机必须满足与在 Visual Studio 中创建 SharePoint 解决方案相同的要求。

 我们还建议安装 [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]。 SDK 包含可用于扩展 Visual Studio 的项目模板和工具。 特别是，SDK 包含可用于轻松创建 Visual Studio 扩展 (VSIX) 包的项目模板。 VSIX 包是在 Visual Studio 中部署 Visual Studio 扩展的首选方法。 所有 SharePoint 工具扩展都必须使用 VSIX 包部署。 本文档中的所有演练均假设已安装 [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]。

 要安装 Visual Studio SDK，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。 有关 Visual Studio 扩展的详细信息，请参阅[开始开发 Visual Studio 扩展](../extensibility/starting-to-develop-visual-studio-extensions.md)。

## <a name="see-also"></a>另请参阅

- [SharePoint 工具扩展的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
- [扩展服务器资源管理器中的“SharePoint 连接”节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [SharePoint 工具扩展的编程概念和功能](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
- [引用（SharePoint 工具扩展）](../sharepoint/reference-sharepoint-tools-extensibility.md)
- [在 Visual Studio 中调试 SharePoint 工具扩展](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)
- [在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)