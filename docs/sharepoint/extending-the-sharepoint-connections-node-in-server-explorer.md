---
title: 扩展 "SharePoint 连接" 节点服务器资源管理器 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62967352"
---
# <a name="extend-the-sharepoint-connections-node-in-server-explorer"></a>扩展中的 "SharePoint 连接" 节点服务器资源管理器
  在 Visual Studio 中，可以使用 "**服务器资源管理器**" 窗口中的 " **SharePoint 连接**" 节点连接到开发计算机上的本地 SharePoint 站点。 此节点在分层树视图中显示本地 SharePoint 站点的多个组件。 例如，你可以在本地站点上查看列表、文档库和内容类型。 有关使用 **服务器资源管理器** 连接到本地 SharePoint 站点的详细信息，请参阅 [使用服务器资源管理器浏览 SharePoint 连接](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)。

 您可以通过为现有节点创建扩展，或通过创建自定义节点类型并将其添加到节点的层次结构中来扩展 " **SharePoint 连接** " 节点。

## <a name="tasks-for-extending-the-sharepoint-connections-node"></a>用于扩展 SharePoint 连接节点的任务
 若要扩展现有节点，请创建用于实现接口的 Visual Studio 扩展 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 。 扩展节点时，可以向节点添加功能，如您自己的快捷菜单项或自定义属性。 有关详细信息，请参阅 [如何：在服务器资源管理器中扩展 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)。

 若要创建自定义节点类型，请创建用于实现接口的 Visual Studio 扩展 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 。 如果要显示默认情况下未显示在 **服务器资源管理器** 中的 SharePoint 站点的组件，请创建自定义节点。 例如，默认情况下， **服务器资源管理器** 不显示 SharePoint 站点的 Web 部件库，但你可以添加一个执行此的自定义节点。 有关详细信息，请参阅 [如何：将自定义 SharePoint 节点添加到服务器资源管理器](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md) 和 [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

## <a name="add-custom-properties-to-nodes"></a>向节点添加自定义属性
 扩展节点或创建自定义节点类型时，可以向节点添加自定义属性。 选择节点时，属性将显示在 " **属性** " 窗口中。

 可以向节点添加两种类型的自定义属性：

- 用于显示 SharePoint 站点中的一组只读数据的属性。 数据描述该节点表示的 SharePoint 组件。 有关演示如何执行此操作的演练，请参阅 [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

- 显示自定义读/写数据的属性。 有关演示如何执行此操作的代码示例，请参阅 [如何：在服务器资源管理器中扩展 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)。

## <a name="get-data-for-built-in-nodes"></a>获取内置节点的数据
 Visual Studio 提供的所有内置节点都包含有关其所表示的 SharePoint 组件的一些数据。 例如，表示 SharePoint 站点上的列表的节点提供了有关列表的一些数据，例如列表的默认视图的标题和 URL。

 若要访问此数据，请从 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> 表示您感兴趣的节点的对象的属性中检索数据对象。 数据对象的类型取决于节点的类型。

 下面的代码示例演示如何获取列表节点的数据对象。 若要在更大的示例上下文中查看此示例，请参阅 [如何：获取服务器资源管理器中内置 SharePoint 节点的数据](../sharepoint/how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer.md)。

 [!code-vb[SPExtensibility.ProjectSystemExtension.General#11](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextensionnodeinfo.vb#11)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#11](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextensionnodeinfo.cs#11)]

 下表列出了每个内置节点类型的数据对象类型。

|节点类型|数据对象类型|
|---------------|----------------------|
|SharePoint 站点节点|<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerSiteNodeInfo>|
|内容类型|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IContentTypeNodeInfo>|
|功能|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IFeatureNodeInfo>|
|字段|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IFieldNodeInfo>|
|列表|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListNodeInfo>|
|列表模板|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListTemplateNodeInfo>|
| (Microsoft.sharepoint.spview 的列表视图) |<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListViewNodeInfo>|
|工作流关联|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IWorkflowAssociationNodeInfo>|
|工作流模板|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IWorkflowTemplateNodeInfo>|

 有关使用属性的详细信息 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> ，请参阅 [将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)。

## <a name="see-also"></a>另请参阅
- [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [如何：在服务器资源管理器中扩展 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [如何：将自定义 SharePoint 节点添加到服务器资源管理器](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)
- [如何：在服务器资源管理器中为内置 SharePoint 节点获取数据](../sharepoint/how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer.md)
- [将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
- [使用服务器资源管理器浏览 SharePoint 连接](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
- [在 Visual Studio 中扩展 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
