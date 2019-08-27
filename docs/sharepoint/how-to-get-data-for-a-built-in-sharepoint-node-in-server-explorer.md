---
title: 在服务器资源管理器中的内置 SharePoint 节点获取数据
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b90582c9b8d352f95d3d5abb3bbb7fb69283b06b
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401427"
---
# <a name="how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer"></a>如何：在服务器资源管理器中的内置 SharePoint 节点获取数据
  在每个内置 SharePoint 节点**服务器资源管理器**，可以为该节点表示的基础 SharePoint 组件获取数据。 有关详细信息，请参阅[扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

## <a name="example"></a>示例
 下面的代码示例演示如何获取基础列表节点表示中的 SharePoint 列表的数据**服务器资源管理器**。 默认情况下，列表节点具有**在浏览器中的查看**上下文菜单项，可以单击以打开 Web 浏览器中的列表。 此示例通过添加扩展节点列表**Visual Studio 中的视图**直接在 Visual Studio 中打开列表的上下文菜单项。 代码访问的节点，以获取要在 Visual Studio 中打开的列表的 URL 的列表数据。

 [!code-vb[SPExtensibility.ProjectSystemExtension.General#10](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextensionnodeinfo.vb#10)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#10](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextensionnodeinfo.cs#10)]

 此示例使用 SharePoint 项目服务获取<xref:EnvDTE.DTE>对象，用于打开列出了在 Visual Studio 中。 有关 SharePoint 项目服务的详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

 若要创建的 SharePoint 节点扩展的基本任务的详细信息，请参阅[如何：扩展服务器资源管理器中的 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- EnvDTE

- Microsoft.VisualStudio.SharePoint

- Microsoft.VisualStudio.SharePoint.Explorer.Extensions

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>将扩展部署
 若要部署**服务器资源管理器**扩展中，创建[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (VSIX) 包的程序集和你想要将与该扩展一起分发的任何其他文件。 有关详细信息，请参阅[部署的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [如何：扩展服务器资源管理器中的 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)
- [部署 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
