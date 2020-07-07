---
title: 在部署或收回 SharePoint 项目时运行代码
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5bd60c9d7b30d4620630d1f6752bd4c7e8bf1182
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016063"
---
# <a name="how-to-run-code-when-a-sharepoint-project-is-deployed-or-retracted"></a>如何：在部署或收回 SharePoint 项目时运行代码
  如果要在部署或收回 SharePoint 项目时执行其他任务，可以处理由 Visual Studio 引发的事件。 有关详细信息，请参阅[扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)。

### <a name="to-run-code-when-a-sharepoint-project-is-deployed-or-retracted"></a>在部署或收回 SharePoint 项目时运行代码

1. 创建项目项扩展、项目扩展或新项目项类型的定义。 有关详细信息，请参阅下列主题：

   - [如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

   - [如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

   - [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. 在扩展中，访问 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> 对象。 有关详细信息，请参阅[如何：检索 SharePoint 项目服务](../sharepoint/how-to-retrieve-the-sharepoint-project-service.md)。

3. 处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.DeploymentStarted> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.DeploymentCompleted> 项目服务的和事件。

4. 在事件处理程序中，使用 <xref:Microsoft.VisualStudio.SharePoint.DeploymentEventArgs> 参数获取有关当前部署会话的信息。 例如，你可以确定当前部署会话中的项目，以及该项目是在部署还是收回。

   下面的代码示例演示如何处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.DeploymentStarted> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.DeploymentCompleted> 项目扩展中的和事件。 部署开始时，此扩展将向 "**输出**" 窗口中写入一条附加消息，并为 SharePoint 项目完成。

   [!code-csharp[SPExtensibility.ProjectSystemExtension.General#12](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/handleprojectdeploymentevents.cs#12)]
   [!code-vb[SPExtensibility.ProjectSystemExtension.General#12](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/handleprojectdeploymentevents.vb#12)]

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- VisualStudio

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署该扩展，请为 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 该程序集创建一个扩展（VSIX）包，并为要使用该扩展分发的任何其他文件创建扩展（VSIX）包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [如何：在执行部署步骤时运行代码](../sharepoint/how-to-run-code-when-deployment-steps-are-executed.md)
