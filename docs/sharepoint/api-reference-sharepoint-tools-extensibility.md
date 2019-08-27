---
title: API 参考 （SharePoint 工具扩展） |Microsoft Docs
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
ms.openlocfilehash: 37639068b74b5d99864871355a8b9ef36906f6cd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62987989"
---
# <a name="api-reference-sharepoint-tools-extensibility"></a>API 参考 （SharePoint 工具扩展）
  本部分包含用于扩展 Visual Studio 中的 SharePoint 工具的 API 参考文档。

## <a name="in-this-section"></a>本节内容
 <xref:Microsoft.VisualStudio.SharePoint>

 包含用于扩展 SharePoint 项目系统的类型。 例如，你可以扩展内置 SharePoint 项目和项目项，也可以创建自己的项目项。

 <xref:Microsoft.VisualStudio.SharePoint.Commands>

 包含可用于创建自定义的类型*SharePoint 命令*。 SharePoint 命令是一个用于从 SharePoint 工具扩展中调入 SharePoint 服务器对象模型的方法。

 <xref:Microsoft.VisualStudio.SharePoint.Deployment>

 包含用于扩展 SharePoint 项目的部署过程的类型。

 <xref:Microsoft.VisualStudio.SharePoint.Explorer>

 包含用于扩展中的 SharePoint 节点的类型**服务器资源管理器**或定义自己的节点的类型。

 <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions>

 包含可用于获取有关内置的信息的类型**服务器资源管理器**表示 SharePoint 站点，例如表示列表、 字段或内容类型的节点上的各个组件的节点。

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

## <a name="see-also"></a>请参阅
- [引用&#40;SharePoint 工具扩展&#41;](../sharepoint/reference-sharepoint-tools-extensibility.md)
- [工具扩展的 SharePoint 的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
- [扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)
