---
title: 扩展服务器资源管理器中的 SharePoint 连接节点 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6b1d461419497a0a45f50f12589cf3ac978a7666
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967352"
---
# <a name="extend-the-sharepoint-connections-node-in-server-explorer"></a>扩展服务器资源管理器中的 SharePoint 连接节点
  在 Visual Studio 中，您可以使用连接到开发计算机上的本地 SharePoint 站点**SharePoint 连接**中的节点**服务器资源管理器**窗口。 此节点显示许多组件的本地 SharePoint 站点层次结构树视图中。 例如，您可以在本地站点上查看列表、 文档库和内容类型。 有关使用详细信息**服务器资源管理器**若要连接到本地 SharePoint 站点，请参阅[使用服务器资源管理器浏览 SharePoint 连接](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)。

 您可以扩展**SharePoint 连接**节点通过创建扩展的现有节点，或通过创建自定义节点类型，并将其添加到节点的层次结构。

## <a name="tasks-for-extending-the-sharepoint-connections-node"></a>用于扩展 SharePoint 连接节点的任务
 若要扩展的现有节点，创建一个 Visual Studio 扩展，实现<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension>接口。 扩展一个节点时，您可以将功能添加到如快捷菜单项或自定义属性节点。 有关详细信息，请参阅[如何：扩展服务器资源管理器中的 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)。

 若要创建自定义节点类型，创建一个 Visual Studio 扩展，实现<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider>接口。 如果你想要显示的不会显示在 SharePoint 站点的组件创建自定义节点**服务器资源管理器**默认情况下。 例如，**服务器资源管理器**不会的显示可以添加 Web 部件库中的默认值，但您在 SharePoint 站点执行此自定义节点。 有关详细信息，请参阅[如何：将自定义 SharePoint 节点添加到服务器资源管理器](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)和[演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

## <a name="add-custom-properties-to-nodes"></a>将自定义属性添加到节点
 当你扩展的节点，或创建自定义节点类型时，可以将自定义属性添加到节点。 属性将显示在**属性**窗口时选择的节点。

 有两种类型的自定义属性可以添加到的节点：

- 显示从 SharePoint 站点的只读数据的一组的属性。 数据描述该节点表示的 SharePoint 组件。 有关演示如何执行此操作的演练，请参阅[演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

- 显示自定义读/写数据的属性。 有关演示如何执行此操作的代码示例，请参阅[如何：扩展服务器资源管理器中的 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)。

## <a name="get-data-for-built-in-nodes"></a>内置节点获取数据
 所有 Visual Studio 提供的内置节点都包括它们所代表的 SharePoint 组件有关的一些数据。 例如，表示 SharePoint 站点上的列表中的节点提供有关列表中，例如标题和列表的默认视图的 URL 的一些数据。

 若要访问此数据，检索来自一个数据对象<xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A>属性的<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode>对象，表示你感兴趣的节点。 数据对象的类型取决于节点的类型。

 下面的代码示例演示如何获取列表节点的数据对象。 若要查看此上下文中的一个更大示例的示例，请参阅[如何：在服务器资源管理器中的内置 SharePoint 节点获取数据](../sharepoint/how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer.md)。

 [!code-vb[SPExtensibility.ProjectSystemExtension.General#11](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextensionnodeinfo.vb#11)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#11](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextensionnodeinfo.cs#11)]

 下表列出了每个内置的节点类型的数据对象类型。

|节点类型|数据对象类型|
|---------------|----------------------|
|SharePoint 站点节点|<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerSiteNodeInfo>|
|内容类型|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IContentTypeNodeInfo>|
|功能|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IFeatureNodeInfo>|
|字段|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IFieldNodeInfo>|
|列表|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListNodeInfo>|
|列表模板|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListTemplateNodeInfo>|
|列表视图 (Microsoft.SharePoint.SPView)|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListViewNodeInfo>|
|工作流关联|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IWorkflowAssociationNodeInfo>|
|工作流模板|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IWorkflowTemplateNodeInfo>|

 有关使用详细信息<xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A>属性，请参阅[关联自定义数据与 SharePoint 工具扩展](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)。

## <a name="see-also"></a>请参阅
- [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [如何：扩展服务器资源管理器中的 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [如何：将自定义 SharePoint 节点添加到服务器资源管理器](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)
- [如何：在服务器资源管理器中的内置 SharePoint 节点获取数据](../sharepoint/how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer.md)
- [将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
- [浏览 SharePoint 连接使用服务器资源管理器](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
- [扩展 Visual Studio 中的 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
