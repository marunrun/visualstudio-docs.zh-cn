---
title: 使用服务器资源管理器浏览 SharePoint 连接 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
f1_keywords:
- VS.SharePointTools.SharePointExplorer.SharePointConnection
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, browsing SharePoint sites
- SharePoint development in Visual Studio, SharePoint Connections
- SharePoint Connections [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: baf580ace98ab14032de1e9a3edf18af2b2cfee8
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016355"
---
# <a name="browse-sharepoint-connections-by-using-server-explorer"></a>使用服务器资源管理器浏览 SharePoint 连接
  你现在可以在**服务器资源管理器**中浏览本地 SharePoint 连接。 通过使用这种方法，您可以在系统上浏览 SharePoint 网站的组件。 SharePoint 站点组件（如列表定义和内容类型）显示在**服务器资源管理器**的树视图中名为 " **SharePoint 连接**" 的节点中。 若要显示**服务器资源管理器**，请在菜单栏上选择 "**查看**  >  **服务器资源管理器**"。 除了显示 SharePoint 网站组件以外，通过使用快捷菜单命令，你还可以移除项、查看它们的属性或刷新树视图。

> [!IMPORTANT]
> 若要浏览 SharePoint 网站，您必须是 SharePoint 网站集的管理员，并且必须以本地计算机管理员身份运行 Visual Studio。 否则，站点将显示在**服务器资源管理器**中，但无法展开其节点。 若要验证你是否是网站集的管理员，请在 web 浏览器中打开站点，打开 "**站点操作**" 菜单，选择 "**站点权限**"，然后在 "**权限：团队站点**" 页上，从功能区上的 "**管理**" 组中选择 "**网站集管理员**" 命令。 如果你是网站集管理员，你的名称将显示在文本框中。 如果 "**网站集管理员**" 命令未显示在功能区上的 "管理" 组中，则您不是网站集的管理员，您必须从站点管理员那里获取适当的权限。

## <a name="server-explorer-nodes"></a>服务器资源管理器节点
 SharePoint 站点的每个组件都由 " **Sharepoint 连接**" 下**服务器资源管理器**树视图中的节点表示。 例如，默认 SharePoint 网站包括称为 "讨论" 的内容类型，它表示在 SharePoint 站点的 "**讨论**" 页中显示的讨论类型。 讨论内容类型包含多个字段。 若要在**服务器资源管理器**中查看这些字段，请展开 " **ContentTypes** " 节点，然后展开 "**讨论**" 节点。 下面是几个字段节点，如正文、讨论主题和标题。

## <a name="node-shortcut-menu-commands"></a>节点快捷菜单命令
 每个节点都有一个快捷菜单，可通过右键单击该节点，或选择该节点，然后选择**Shift** + **F10**键来访问它。 节点命令可能包括以下内容：

|命令名：|说明|
|------------------|-----------------|
|刷新|更新树视图，以反映自上次显示节点以来可能发生的任何更改。|
|删除|从树视图中删除选定的节点。 **注意：** 此命令仅在 " **Sharepoint 连接**" 节点下列出的 sharepoint 连接上启用。|
|属性|显示 "**属性**" 窗口中所选节点的可用属性。 属性都是只读的，并且不是每个节点都具有关联的属性。|
|添加连接|允许您指定要浏览的 SharePoint 站点。 在 " **SharePoint 连接**" 节点和子站点节点上可用。|
|在浏览器中查看|在 Web 浏览器中显示所选列表。 对于**列表和库**中包含的 "**列表**" 节点下的某些列表，此命令可用。|

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[如何：添加或删除 SharePoint 连接](../sharepoint/how-to-add-or-remove-sharepoint-connections.md)|描述将新的 SharePoint 站点添加到**服务器资源管理器**中的 " **SharePoint 连接**" 节点所需的步骤。|

## <a name="see-also"></a>另请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
