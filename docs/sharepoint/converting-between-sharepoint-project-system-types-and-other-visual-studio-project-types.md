---
title: 将转换：与其他类型的 SharePoint 项目系统类型
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project service
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 40ea60a8df5bc0bcd033c60a83d742ed3249cc53
ms.sourcegitcommit: cc5fd59e5dc99181601b7db8b28d7f8a83a36bab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2019
ms.locfileid: "66835998"
---
# <a name="convert-between-sharepoint-project-system-types-and-other-visual-studio-project-types"></a>SharePoint 项目系统类型与其他 Visual Studio 项目类型之间转换
  在某些情况下可能会在 SharePoint 项目系统中有一个对象，并且你想要使用的 Visual Studio 自动化对象模型或集成对象模型中的相应对象的功能，反之亦然。 在这些情况下，你可以使用<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A>SharePoint 项目服务将对象转换为不同的对象模型的方法。

 例如，可能有<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>对象，但您想要使用仅可用在方法<xref:EnvDTE.Project>或<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>对象。 在这种情况下，可以使用<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A>方法将转换<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>到<xref:EnvDTE.Project>或<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>。

 有关 Visual Studio 自动化对象模型和 Visual Studio 集成对象模型的详细信息，请参阅[概述的编程模型的 SharePoint 工具扩展](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)。

## <a name="types-of-conversions"></a>类型的转换
 下表列出了此方法可以将 SharePoint 项目系统和其他 Visual Studio 对象模型之间转换的类型。

|SharePoint 项目系统类型|自动化和集成对象模型中的相应类型|
|------------------------------------|-------------------------------------------------------------------------|
|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>|<xref:EnvDTE.Project><br /><br /> 或<br /><br /> 在 Visual Studio 集成对象模型由项目的基础 COM 对象实现任何接口。 这些接口包括<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>， <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> （或派生的接口），和<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>。 由项目实现的主要接口的列表，请参阅[项目模型核心组件](../extensibility/internals/project-model-core-components.md)。|
|<xref:Microsoft.VisualStudio.SharePoint.IMappedFolder><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFile><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeature><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeatureResourceFile><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectPackage>|<xref:EnvDTE.ProjectItem><br /><br /> 或<br /><br /> 一个<xref:System.UInt32>标识中的项目成员的值 （也称为 VSITEMID）<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>包含它。 此值可以传递给*itemid*参数的一些<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>方法。|

## <a name="example"></a>示例
 下面的代码示例演示如何使用<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A>方法将转换<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>对象传递给<xref:EnvDTE.Project>。

 [!code-csharp[SPExtensibility.ProjectService.FromDTE#2](../sharepoint/codesnippet/CSharp/spprojectserviceaddin/connect.cs#2)]
 [!code-vb[SPExtensibility.ProjectService.FromDTE#2](../sharepoint/codesnippet/VisualBasic/spprojectserviceaddin/connect.vb#2)]

 此示例需要：

- 具有对引用的 SharePoint 项目系统的扩展*EnvDTE.dll*程序集。 有关详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

- 注册的代码`projectService_ProjectAdded`方法以处理<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectAdded>事件的<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService>对象。 有关示例，请参见 [如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)。

## <a name="see-also"></a>请参阅

- [使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)
- [如何：检索 SharePoint 项目服务](../sharepoint/how-to-retrieve-the-sharepoint-project-service.md)
- [工具扩展的 SharePoint 的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
