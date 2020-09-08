---
title: 使用服务器资源管理器浏览 SharePoint 连接 | Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86016355"
---
# <a name="browse-sharepoint-connections-by-using-server-explorer"></a>使用服务器资源管理器浏览 SharePoint 连接
  你现在可以在“服务器资源管理器”中浏览本地 SharePoint 连接。 通过使用这种方法，您可以在系统上浏览 SharePoint 网站的组件。 SharePoint 网站组件（例如列表定义和内容类型）显示在“服务器资源管理器”树状视图中一个名为“SharePoint 连接”的节点中 。 若要显示“服务器资源管理器”，请在菜单栏上选择“视图” > “服务器资源管理器”  。 除了显示 SharePoint 网站组件以外，通过使用快捷菜单命令，你还可以移除项、查看它们的属性或刷新树视图。

> [!IMPORTANT]
> 若要浏览 SharePoint 网站，您必须是 SharePoint 网站集的管理员，并且必须以本地计算机管理员身份运行 Visual Studio。 否则，虽然网站会显示在“服务器资源管理器”中，但你不能展开其节点。 若要验证你是否是网站集的管理员，请在 Web 浏览器中打开网站，打开“网站操作”菜单，选择“网站权限”，然后在“权限：  **团队网站”页中，在功能区上的“管理”组中选择“网站集管理员”命令**  。 如果你是网站集管理员，文本框中会显示你的名称。 如果“网站集管理员”命令未显示在功能区的“管理”组中，则你不是网站集的管理员，必须从网站管理员处获取适当的权限。

## <a name="server-explorer-nodes"></a>服务器资源管理器节点
 SharePoint 网站的每个组件均由“服务器资源管理器”树状视图中“SharePoint 连接”下的节点表示 。 例如，默认的 SharePoint 网站包括名为“讨论”的内容类型，它表示显示在 SharePoint 网站“讨论”页中的讨论类型。 讨论内容类型包含多个字段。 若要在“服务器资源管理器”中查看这些字段，请展开“内容类型”节点，再展开“讨论”节点  。 下面是几个字段节点，如正文、讨论主题和标题。

## <a name="node-shortcut-menu-commands"></a>节点快捷菜单命令
 每个节点都有一个快捷菜单，可通过右击该节点或选择该节点并选择 Shift+F10 来访问快捷菜单 。 节点命令可能包括以下各项：

|命令名：|说明|
|------------------|-----------------|
|刷新|更新树状视图以反映自上次显示节点以来可能发生的任何更改。|
|删除|从树状视图窗格中删除所选节点。 **注意：** 仅在“SharePoint 连接”节点下列出的 SharePoint 连接上启用此命令。|
|属性|在“属性”窗口中显示所选节点的可用属性。 这些属性都是只读的，并且并非每个节点都具有与其关联的属性。|
|添加连接|可指定要浏览的 SharePoint 网站。 在 SharePoint 连接节点和子站点节点上可用。|
|在浏览器中查看|在 Web 浏览器中显示所选列表。 此命令可用于“列表”节点下的某些列表，该节点包含在“列表和库”中 。|

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[如何：添加或删除 SharePoint 连接](../sharepoint/how-to-add-or-remove-sharepoint-connections.md)|描述向“服务器资源管理器”中的“SharePoint 连接”节点添加新的 SharePoint 网站所需的步骤 。|

## <a name="see-also"></a>另请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
