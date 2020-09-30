---
title: Convert： SharePoint 项目系统类型与其他类型之间的转换
titleSuffix: ''
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
ms.openlocfilehash: 44b3e32114b10eae776f39e4c3d7337bba636f3f
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584641"
---
# <a name="convert-between-sharepoint-project-system-types-and-other-visual-studio-project-types"></a>在 SharePoint 项目系统类型和其他 Visual Studio 项目类型之间转换
  在某些情况下，您可能在 SharePoint 项目系统中有一个对象，并且您想要使用 Visual Studio 自动化对象模型或集成对象模型中的相应对象的功能，反之亦然。 在这些情况下，可以使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A> SharePoint 项目服务的方法将对象转换为不同的对象模型。

 例如，你可能有一个 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> 对象，但你想要使用仅在或对象上可用的方法 <xref:EnvDTE.Project> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> 。 在这种情况下，可以使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A> 方法将转换 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> 为 <xref:EnvDTE.Project> 或 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> 。

 有关 Visual Studio 自动化对象模型和 Visual Studio 集成对象模型的详细信息，请参阅 [SharePoint 工具扩展的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)。

## <a name="types-of-conversions"></a>转换类型
 下表列出了此方法可在 SharePoint 项目系统和其他 Visual Studio 对象模型之间进行转换的类型。

|SharePoint 项目系统类型|自动化和集成对象模型中的相应类型|
|------------------------------------|-------------------------------------------------------------------------|
|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>|<xref:EnvDTE.Project><br /><br /> 或<br /><br /> Visual Studio 集成对象模型中由项目的基础 COM 对象实现的任何接口。 这些接口包括 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> (或派生接口) 、和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> 。 有关项目实现的主接口的列表，请参阅 [项目模型核心组件](../extensibility/internals/project-model-core-components.md)。|
|<xref:Microsoft.VisualStudio.SharePoint.IMappedFolder><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFile><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeature><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeatureResourceFile><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectPackage>|<xref:EnvDTE.ProjectItem><br /><br /> 或<br /><br /> <xref:System.UInt32>值 (也称为 VSITEMID) ，用于标识包含它的中的项目成员 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 。 此值可传递给某些方法的 *itemid* 参数 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 。|

## <a name="example"></a>示例
 下面的代码示例演示如何使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A> 方法将 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> 对象转换为 <xref:EnvDTE.Project> 。

 [!code-csharp[SPExtensibility.ProjectService.FromDTE#2](../sharepoint/codesnippet/CSharp/spprojectserviceaddin/connect.cs#2)]
 [!code-vb[SPExtensibility.ProjectService.FromDTE#2](../sharepoint/codesnippet/VisualBasic/spprojectserviceaddin/connect.vb#2)]

 此示例需要：

- 具有对 *EnvDTE.dll* 程序集的引用的 SharePoint 项目系统的扩展。 有关详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

- 注册 `projectService_ProjectAdded` 方法以处理对象的事件的代码 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectAdded> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> 。 有关示例，请参阅 [如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)。

## <a name="see-also"></a>另请参阅

- [使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)
- [如何：检索 SharePoint 项目服务](../sharepoint/how-to-retrieve-the-sharepoint-project-service.md)
- [SharePoint 工具扩展的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
