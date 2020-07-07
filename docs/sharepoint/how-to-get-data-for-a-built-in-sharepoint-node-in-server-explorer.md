---
title: 获取服务器资源管理器中内置 SharePoint 节点的数据
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 5bb69773bf3f031b75d63ebe8cb1f1b4a00286c9
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014890"
---
# <a name="how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer"></a>如何：在服务器资源管理器中为内置 SharePoint 节点获取数据
  对于**服务器资源管理器**中的每个内置 sharepoint 节点，你可以获取该节点表示的基础 sharepoint 组件的数据。 有关详细信息，请参阅[服务器资源管理器中的 "扩展 SharePoint 连接" 节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

## <a name="example"></a>示例
 下面的代码示例演示如何获取列表节点在**服务器资源管理器**中表示的基础 SharePoint 列表的数据。 默认情况下，列表节点**在浏览器**上下文菜单项中有一个视图，您可以单击它在 Web 浏览器中打开列表。 此示例通过添加 visual Studio 上下文菜单项**中的视图，在**visual studio 中直接打开列表，来扩展列表节点。 此代码访问节点的列表数据，以获取要在 Visual Studio 中打开的列表的 URL。

 [!code-vb[SPExtensibility.ProjectSystemExtension.General#10](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextensionnodeinfo.vb#10)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#10](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextensionnodeinfo.cs#10)]

 此示例使用 SharePoint 项目服务获取 <xref:EnvDTE.DTE> 用于在 Visual Studio 中打开列表的对象。 有关 SharePoint 项目服务的详细信息，请参阅[使用 sharepoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

 有关为 SharePoint 节点创建扩展的基本任务的详细信息，请参阅[如何：在服务器资源管理器中扩展 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- EnvDTE

- VisualStudio

- VisualStudio （Extension）

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署**服务器资源管理器**扩展，请为 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 程序集以及要使用该扩展分发的任何其他文件创建扩展（VSIX）包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [扩展中的 "SharePoint 连接" 节点服务器资源管理器](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [如何：在服务器资源管理器中扩展 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)
- [在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
