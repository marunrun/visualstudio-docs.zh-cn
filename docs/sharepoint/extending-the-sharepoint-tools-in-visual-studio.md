---
title: 扩展 Visual Studio 中的 SharePoint 工具 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 7d70d9b5bac260dc0731d06ebb11780114f0edf5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967417"
---
# <a name="extend-the-sharepoint-tools-in-visual-studio"></a>扩展 Visual Studio 中的 SharePoint 工具
  Visual Studio 中的 SharePoint 工具满足许多应用程序开发方案的要求。 但是，可能会发现它们不提供你或其他开发人员需要的功能的情况。 在这些情况下，您可以扩展 SharePoint 工具以创建所需的功能。

## <a name="how-to-extend-the-sharepoint-tools"></a>如何扩展 SharePoint 工具
 您可以扩展 SharePoint 项目系统和**SharePoint 连接**中的节点**服务器资源管理器**窗口。

### <a name="extend-the-sharepoint-project-system"></a>扩展 SharePoint 项目系统
 Visual Studio 包含一组项目模板和项模板可用于创建 SharePoint 解决方案。 例如，有事件接收器、 列表定义、 工作流和 Web 部件的模板。 但是，您还可以定义自己的用于创建 SharePoint 组件，例如字段或自定义操作的 SharePoint 项目项的类型。 您还可以创建在 Visual Studio 中，已安装的 SharePoint 项目项类型的扩展，并且可以创建扩展 SharePoint 项目。

 有关详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

### <a name="extend-the-sharepoint-connections-node-in-server-explorer"></a>扩展服务器资源管理器中的 SharePoint 连接节点
 在 Visual Studio 中，你可以使用**SharePoint 连接**中的节点**服务器资源管理器**窗口以分层树视图中查看许多组件的一个或多个本地 SharePoint 站点。 您还可以扩展**SharePoint 连接**节点中的以下方法：

- 通过添加自己的节点。 这是你想要显示的 SharePoint 网站的默认情况下不显示组件的情况下很有用。

- 通过扩展现有节点。 例如，可以将新的子节点添加到现有节点，或者可以添加到节点的快捷菜单项和开发人员单击菜单项时执行任务。

  有关详细信息，请参阅[扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

## <a name="development-computer-requirements"></a>开发计算机要求
 若要创建 SharePoint 工具扩展，在开发计算机必须满足相同要求的 Visual Studio 中创建 SharePoint 解决方案。

 我们还建议您安装[!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]。 SDK 包括项目模板和工具，可用于扩展 Visual Studio。 具体而言，该 SDK 包括可用于轻松地创建 Visual Studio 扩展 (VSIX) 包的项目模板。 VSIX 包是部署在 Visual Studio 中的 Visual Studio 扩展的首选的方法。 必须使用 VSIX 包来部署所有 SharePoint 工具扩展。 所有本文档中的演练假定您已[!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]安装。

 若要安装 Visual Studio SDK，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。 有关 Visual Studio 扩展的详细信息，请参阅[开始开发 Visual Studio 扩展到](../extensibility/starting-to-develop-visual-studio-extensions.md)。

## <a name="see-also"></a>请参阅

- [工具扩展的 SharePoint 的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
- [扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [SharePoint 工具扩展的编程概念和功能](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
- [引用&#40;SharePoint 工具扩展&#41;](../sharepoint/reference-sharepoint-tools-extensibility.md)
- [调试 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)
- [部署 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)