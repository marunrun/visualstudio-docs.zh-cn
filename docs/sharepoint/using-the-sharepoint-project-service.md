---
title: 使用 SharePoint 项目服务 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project service
- SharePoint development in Visual Studio, extensibility features
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4dfb7592fb2cec05da1bd72bd69a76e9a3b270db
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "63007934"
---
# <a name="use-the-sharepoint-project-service"></a>使用 SharePoint 项目服务
  SharePoint 项目系统包括一项可以用于执行项目系统相关任务的项目服务。 该项目服务是一个 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> 对象。

 你可以在任何 SharePoint 工具扩展中访问该 SharePoint 项目服务。 你还可在其他类型的 Visual Studio 中访问该项目服务，例如加载项和 VSPackage。 有关详细信息，请参阅 [如何：检索 SharePoint 项目服务](../sharepoint/how-to-retrieve-the-sharepoint-project-service.md)。

## <a name="project-service-features"></a>项目服务功能
 下表列出了你可以使用 SharePoint 项目服务执行的任务，以及用于执行每项任务的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> 方法或属性。

|任务|供使用的成员|
|----------|-------------------|
|访问在 Visual Studio 中打开的任何 SharePoint 项目。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Projects%2A> 属性。|
|访问可用的所有 SharePoint 项目项类型（包括内置和自定义项目项类型）。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.ProjectItemTypes%2A> 属性。|
|访问可供  SharePoint 项目使用的所有部署步骤（包括内置和自定义部署步骤）。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.DeploymentSteps%2A> 属性。|
|访问开发人员重构 SharePoint 项目中的代码时引发的事件。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.CodeRefactoringEvents%2A> 属性。|
|执行调入 SharePoint 服务器对象模型的自定义 *sharepoint 命令* 。 有关 SharePoint 命令的详细信息，请参阅 [调入 sharepoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.SharePointConnection%2A> 属性。|
|将 SharePoint 项目系统中的类型转换为 Visual Studio 自动化对象模型或集成对象模型中的类型，反之亦然。 有关详细信息，请参阅 [在 SharePoint 项目系统类型和其他 Visual Studio 项目类型之间转换](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A> 方法。|
|将消息写入到 " **输出** " 窗口，或在 Visual Studio 中 **错误列表** "窗口。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Logger%2A> 属性。|
|访问 Visual Studio 中可用的其他服务。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.ServiceProvider%2A> 属性。|
|检索用于调试解决方案的本地 SharePoint 站点的安装文件夹的路径。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.SharePointInstallPath%2A> 属性。|
|确定 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] 或 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] 是否已在计算机上安装。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.IsSharePointInstalled%2A> 属性。|
|验证 SharePoint 解决方案中的功能或包。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.PackageValidationProvider%2A> 属性。|

## <a name="see-also"></a>另请参阅
- [在 SharePoint 项目系统类型和其他 Visual Studio 项目类型之间转换](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)
- [如何：检索 SharePoint 项目服务](../sharepoint/how-to-retrieve-the-sharepoint-project-service.md)
- [在 Visual Studio 中扩展 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
- [SharePoint 工具扩展的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
- [如何：从 DTE 对象获取服务](https://msdn.microsoft.com/library/bb166401.aspx)
