---
title: 如何：检索 SharePoint 项目服务 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: f49883337c5748c0f8bcab5d0a88e02612e51b4c
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015553"
---
# <a name="how-to-retrieve-the-sharepoint-project-service"></a>如何：检索 SharePoint 项目服务
  您可以使用以下类型的解决方案访问 SharePoint 项目服务：

- SharePoint 项目系统的扩展，例如项目扩展、项目项扩展或项目项类型定义。 有关这些类型的扩展的详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

- **服务器资源管理器**中的 " **SharePoint 连接**" 节点的扩展。 有关这些类型的扩展的详细信息，请参阅[服务器资源管理器中的 "扩展 SharePoint 连接" 节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

- Visual Studio 扩展的另一种类型，如 VSPackage。

## <a name="retrieve-the-service-in-project-system-extensions"></a>检索项目系统扩展中的服务
 在任何 SharePoint 项目系统的扩展中，你都可以使用对象的属性访问项目服务 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectService%2A> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> 。

 你还可以使用以下过程检索项目服务。

#### <a name="to-retrieve-the-service-in-a-project-extension"></a>在项目扩展中检索服务

1. 在接口的实现中 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> ，找到 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> 方法。

2. 使用*projectService*参数访问服务。

     下面的代码示例演示如何使用项目服务将消息写入到 "**输出**" 窗口，并在简单的项目扩展中**错误列表**"窗口。

     [!code-vb[SPExtensibility.ProjectService.FromProjectSystemExtensions#1](../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb#1)]
     [!code-csharp[SPExtensibility.ProjectService.FromProjectSystemExtensions#1](../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs#1)]

     有关创建项目扩展的详细信息，请参阅[如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)。

#### <a name="to-retrieve-the-service-in-a-project-item-extension"></a>检索项目项扩展中的服务

1. 在接口的实现中 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> ，找到 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> 方法。

2. 使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType.ProjectService%2A> *projectItemType*参数的属性检索服务。

     下面的代码示例演示如何使用项目服务将消息写入到 "**输出**" 窗口，并在 "**列表定义**" 项目项的简单扩展中**错误列表**"窗口。

     [!code-vb[SPExtensibility.ProjectService.FromProjectSystemExtensions#2](../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb#2)]
     [!code-csharp[SPExtensibility.ProjectService.FromProjectSystemExtensions#2](../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs#2)]

     有关创建项目项扩展的详细信息，请参阅[如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)。

#### <a name="to-retrieve-the-service-in-a-project-item-type-definition"></a>在项目项类型定义中检索服务

1. 在接口的实现中 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> ，找到 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> 方法。

2. 使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.ProjectService%2A> *typeDefinition*参数的属性检索服务。

     下面的代码示例演示如何使用项目服务将消息写入到 "**输出**" 窗口，并在简单项目项类型定义中**错误列表**"窗口。

     [!code-vb[SPExtensibility.ProjectService.FromProjectSystemExtensions#3](../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb#3)]
     [!code-csharp[SPExtensibility.ProjectService.FromProjectSystemExtensions#3](../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs#3)]

     有关定义项目项类型的详细信息，请参阅[如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

## <a name="retrieve-the-service-in-server-explorer-extensions"></a>检索服务器资源管理器扩展中的服务
 在**服务器资源管理器**的 " **SharePoint 连接**" 节点的扩展中，可以通过使用对象的属性来访问项目服务 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.ServiceProvider%2A> <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> 。

#### <a name="to-retrieve-the-service-in-a-server-explorer-extension"></a>在服务器资源管理器扩展中检索服务

1. 获取 <xref:System.IServiceProvider> <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.ServiceProvider%2A> <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> 扩展中对象的属性中的对象。

2. 使用 <xref:System.IServiceProvider.GetService%2A> 方法请求 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> 对象。

     下面的代码示例演示如何使用项目服务将消息写入到 "**输出**" 窗口，并从扩展添加到**服务器资源管理器**中的列表节点的快捷菜单中**错误列表**"窗口。

     [!code-vb[SPExtensibility.ProjectService.FromSPExplorerExtensions#1](../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromspexplorerextensions.getprojectservice/extension/extension.vb#1)]
     [!code-csharp[SPExtensibility.ProjectService.FromSPExplorerExtensions#1](../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromspexplorerextensions.getprojectservice/extension/extension.cs#1)]

     有关**服务器资源管理器**中扩展**sharepoint 连接**节点的详细信息，请参阅[如何：在服务器资源管理器中扩展 sharepoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)。

## <a name="retrieve-the-service-in-other-visual-studio-extensions"></a>在其他 Visual Studio 扩展中检索服务
 可以在 VSPackage 中检索项目服务，或在可访问自动化对象模型中的对象的任何 Visual Studio 扩展中检索项目服务 <xref:EnvDTE80.DTE2> ，例如实现接口的项目模板向导 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 。

 在 VSPackage 中，可以 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> 使用以下方法之一来请求对象：

- <xref:System.IServiceProvider.GetService%2A>派生自类的托管 VSPackage 的方法 <xref:Microsoft.VisualStudio.Shell.Package> 。 有关详细信息，请参阅[如何：获取服务](../extensibility/how-to-get-a-service.md)。

- 静态 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 方法。 有关详细信息，请参阅[Use GetGlobalService](../extensibility/internals/service-essentials.md#how-to-use-getglobalservice)。

  在有权访问对象的 Visual Studio 扩展中 <xref:EnvDTE80.DTE2> ，可以 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> 使用对象的方法请求对象 <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> <xref:Microsoft.VisualStudio.Shell.ServiceProvider> 。 有关详细信息，请参阅[从 DTE 对象获取服务](../extensibility/how-to-get-a-service.md#getting-a-service-from-the-dte-object)。

## <a name="see-also"></a>另请参阅
- [使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)
- [如何：获取服务](../extensibility/how-to-get-a-service.md)
- [如何：将向导与项目模板结合使用](../extensibility/how-to-use-wizards-with-project-templates.md)
