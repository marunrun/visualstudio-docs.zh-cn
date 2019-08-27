---
title: 在部署或收回 SharePoint 项目时运行代码
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 9e3f46ff9d2e83307f745180288e69839a0d336e
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401755"
---
# <a name="how-to-run-code-when-a-sharepoint-project-is-deployed-or-retracted"></a>如何：在部署或收回 SharePoint 项目时运行代码
  如果你想要部署或收回 SharePoint 项目时执行其他任务，可以处理由 Visual Studio 引发事件。 有关详细信息，请参阅[扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)。

### <a name="to-run-code-when-a-sharepoint-project-is-deployed-or-retracted"></a>若要运行代码的 SharePoint 项目时部署或收回

1. 创建项目项扩展、 项目扩展或新的项目项类型的定义。 有关详细信息，请参阅下列主题：

   - [如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

   - [如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

   - [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. 在扩展中，访问<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService>对象。 有关详细信息，请参阅[如何：检索 SharePoint 项目服务](../sharepoint/how-to-retrieve-the-sharepoint-project-service.md)。

3. 处理<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.DeploymentStarted>和<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.DeploymentCompleted>项目服务的事件。

4. 在事件处理程序，使用<xref:Microsoft.VisualStudio.SharePoint.DeploymentEventArgs>参数，以获取有关当前部署会话的信息。 例如，可以确定哪些项目是在当前部署会话中，而且是否正在部署或收回。

   下面的代码示例演示如何处理<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.DeploymentStarted>和<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.DeploymentCompleted>项目扩展中的事件。 此扩展将写入到的其他消息**输出**部署开始和完成的 SharePoint 项目时的窗口。

   [!code-csharp[SPExtensibility.ProjectSystemExtension.General#12](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/handleprojectdeploymentevents.cs#12)]
   [!code-vb[SPExtensibility.ProjectSystemExtension.General#12](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/handleprojectdeploymentevents.vb#12)]

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>将扩展部署
 若要将扩展部署，创建[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (VSIX) 包的程序集和你想要将与该扩展一起分发的任何其他文件。 有关详细信息，请参阅[部署的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [如何：执行部署步骤时运行代码](../sharepoint/how-to-run-code-when-deployment-steps-are-executed.md)
