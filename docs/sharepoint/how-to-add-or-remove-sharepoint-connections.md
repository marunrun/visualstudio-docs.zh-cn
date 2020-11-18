---
title: 如何：添加或删除 SharePoint 连接 |Microsoft Docs
description: 使用 Visual Studio 的 "服务器资源管理器" 窗口中的 "SharePoint 连接" 节点添加或删除 SharePoint 连接。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: b898dd0f9327c7589d0dac3436aec0299009221d
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850710"
---
# <a name="how-to-add-or-remove-sharepoint-connections"></a>如何：添加或删除 SharePoint 连接
  服务器资源管理器使你可以浏览 SharePoint 站点以及数据连接。 但是，必须先将 SharePoint 站点的内容添加到 **sharepoint "连接** " 节点中，然后才能浏览该站点的内容。

### <a name="to-add-a-sharepoint-site-to-the-sharepoint-connections-node"></a>将 SharePoint 站点添加到 "SharePoint 连接" 节点

1. 在菜单栏上，依次选择 " **视图**"、" **服务器资源管理器**"。

2. 在 **服务器资源管理器** 中，选择 " **SharePoint 连接**" 节点，然后在菜单栏上选择 "**工具**" "  >  **添加 SharePoint 连接**"。

3. 在 " **添加 Sharepoint 连接** " 框中，输入 [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] sharepoint 站点的 (例如， http://testserver/sites/unittests) 。

### <a name="to-delete-a-sharepoint-site-from-the-sharepoint-connections-node"></a>从 "SharePoint 连接" 节点中删除 SharePoint 站点

1. 在菜单栏上，依次选择 " **视图**"、" **服务器资源管理器** " 以打开 **服务器资源管理器**。

2. 展开 " **Sharepoint 连接** " 节点以显示要从 **服务器资源管理器** 中删除的 sharepoint 站点。

3. 选择站点，然后在菜单栏上选择 "编辑" " **Edit**  >  **删除**"。

    > [!NOTE]
    > 此步骤不会删除基础站点;它仅删除 **服务器资源管理器** 的连接。

## <a name="see-also"></a>另请参阅
- [使用服务器资源管理器浏览 SharePoint 连接](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
