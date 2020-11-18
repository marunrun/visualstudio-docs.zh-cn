---
title: " (SharePoint 工具扩展性的 API 参考) |Microsoft Docs"
description: 查看 API 参考文档，了解如何在 Visual Studio 中扩展 SharePoint 工具。 查看相关命名空间（如 VisualStudio）的列表。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, reference for project and tools extensibility
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4599a2c305558f2ef551d19abac210bdf05269f3
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850385"
---
# <a name="api-reference-sharepoint-tools-extensibility"></a> (SharePoint 工具扩展性的 API 参考) 
  本部分包含有关在 Visual Studio 中扩展 SharePoint 工具的 API 参考文档。

## <a name="in-this-section"></a>在此部分中
 <xref:Microsoft.VisualStudio.SharePoint>

 包含用于扩展 SharePoint 项目系统的类型。 例如，你可以扩展内置 SharePoint 项目和项目项，也可以创建自己的项目项。

 <xref:Microsoft.VisualStudio.SharePoint.Commands>

 包含可用于创建自定义 *SharePoint 命令* 的类型。 SharePoint 命令是一个用于从 SharePoint 工具扩展中调入 SharePoint 服务器对象模型的方法。

 <xref:Microsoft.VisualStudio.SharePoint.Deployment>

 包含用于扩展 SharePoint 项目的部署过程的类型。

 <xref:Microsoft.VisualStudio.SharePoint.Explorer>

 包含用来在 **服务器资源管理器** 中扩展 SharePoint 节点或定义您自己的节点类型的类型。

 <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions>

 包含可用于获取有关内置 **服务器资源管理器** 节点的信息的类型，这些节点表示 SharePoint 站点上的单个组件，如表示列表、字段或内容类型的节点。

 <xref:Microsoft.VisualStudio.SharePoint.Features>

 包含用于访问 SharePoint 项目中的功能定义的类型。

 <xref:Microsoft.VisualStudio.SharePoint.Packages>

 包含用于访问 SharePoint 项目中的包定义的类型。

 <xref:Microsoft.VisualStudio.SharePoint.Remote.Authentication>

 包含用于对部署到远程 SharePoint 网站的 SharePoint 应用进行身份验证并与其通信的类型。

 <xref:Microsoft.VisualStudio.SharePoint.Remote.Commands>

 包含用于创建 SharePoint 远程命令以对部署到远程 SharePoint 网站的 SharePoint 应用使用的类型。

 <xref:Microsoft.VisualStudio.SharePoint.Tasks>

 包含 Visual Studio 用作生成任务以打包和调试 SharePoint 项目、Office 应用和 SharePoint 应用的类型。 此 API 支持 Office 和 SharePoint 基础结构，不应在代码中直接使用。

 <xref:Microsoft.VisualStudio.SharePoint.Validation>

 包含用于为 SharePoint 项目自定义功能和包验证行为的类型。

## <a name="see-also"></a>另请参阅
- [SharePoint 工具扩展性 &#40;引用&#41;](../sharepoint/reference-sharepoint-tools-extensibility.md)
- [SharePoint 工具扩展的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
- [扩展服务器资源管理器中的“SharePoint 连接”节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)
