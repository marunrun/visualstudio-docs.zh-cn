---
title: 使用服务器资源管理器浏览 SharePoint 连接 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 8dfde37125b78e2ff8077712321b3a19816582cf
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387808"
---
# <a name="browse-sharepoint-connections-by-using-server-explorer"></a>通过使用服务器资源管理器浏览 SharePoint 连接
  你现在可以浏览中的本地 SharePoint 连接**服务器资源管理器**。 通过使用这种方法，您可以在系统上浏览 SharePoint 网站的组件。 SharePoint 网站组件，例如列表定义和内容类型出现在名为节点**SharePoint 连接**中的树视图**服务器资源管理器**。 若要显示**服务器资源管理器**，在菜单栏上依次选择**视图** > **服务器资源管理器**。 除了显示 SharePoint 网站组件以外，通过使用快捷菜单命令，你还可以移除项、查看它们的属性或刷新树视图。

> [!IMPORTANT]
> 若要浏览 SharePoint 网站，您必须是 SharePoint 网站集的管理员，并且必须以本地计算机管理员身份运行 Visual Studio。 否则，站点会显示在**服务器资源管理器**，但不能展开其节点。 若要验证你是否是站点集合的管理员，请打开站点在 web 浏览器打开**站点操作**菜单中，选择**站点权限**，然后在**权限：团队网站**页上，选择**网站集管理员**命令**管理**组功能区上。 如果您是网站集管理员，你的名称将显示在文本框中。 如果**网站集管理员**命令未出现在功能区上的管理组中，你不是站点集合管理员和必须从站点管理员获取相应的权限。

## <a name="server-explorer-nodes"></a>服务器资源管理器节点
 中的节点所表示的 SharePoint 网站，每个部分**服务器资源管理器**树视图下的**SharePoint 连接**。 例如，默认 SharePoint 站点包括一个名为讨论，表示在显示的讨论类型的内容类型**讨论**在 SharePoint 站点的页面。 讨论内容类型包含多个字段。 若要查看中的这些字段**服务器资源管理器**，展开**ContentTypes**节点，然后**讨论**节点。 下它是多个字段节点，如正文、 讨论主题和标题。

## <a name="node-shortcut-menu-commands"></a>节点的快捷菜单命令
 每个节点具有访问通过右键单击节点或选择它，然后选择快捷菜单**Shift**+**F10**密钥。 节点命令可能包括：

|命令名：|描述|
|------------------|-----------------|
|刷新|更新以反映自上次已显示该节点可能已发生任何更改在树视图。|
|删除|从树视图中删除所选的节点。 **注意：** 此命令仅在下列出的 SharePoint 连接上启用**SharePoint 连接**节点。|
|属性|显示在所选节点的可用属性**属性**窗口。 属性是只读的且不是每个节点均具有相关联的属性。|
|添加连接|可以指定你想要浏览的 SharePoint 站点。 可在上找到**SharePoint 连接**节点和子站点节点。|
|在浏览器中查看|在 Web 浏览器中显示所选的列表。 此命令将用下的某些列表**列出了**节点中包含**列表和库**。|

## <a name="related-topics"></a>相关主题

|标题|说明|
|-----------|-----------------|
|[如何：添加或删除 SharePoint 连接](../sharepoint/how-to-add-or-remove-sharepoint-connections.md)|描述所需的添加到新的 SharePoint 站点的步骤**SharePoint 连接**中的节点**服务器资源管理器**。|

## <a name="see-also"></a>请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
