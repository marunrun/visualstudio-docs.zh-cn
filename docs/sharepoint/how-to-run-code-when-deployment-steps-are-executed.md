---
title: 如何：执行运行的代码时部署步骤 |Microsoft Docs
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
ms.openlocfilehash: 581f9c0b9907fd59863f6a468a45ef67d9966475
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62813147"
---
# <a name="how-to-run-code-when-deployment-steps-are-executed"></a>如何：执行部署步骤时运行代码
  如果你想要为 SharePoint 项目中的部署步骤执行其他任务，则可以处理之前的 SharePoint 项目项和 Visual Studio 执行每个部署步骤之后引发的事件。 有关详细信息，请参阅[扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)。

### <a name="to-run-code-when-deployment-steps-are-executed"></a>若要执行部署步骤时运行代码

1. 创建项目项扩展、 项目扩展或新的项目项类型的定义。 有关详细信息，请参阅下列主题：

    - [如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

    - [如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

    - [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. 在扩展中，处理<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted>并<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepCompleted>的事件<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType>（在项目项扩展或项目扩展） 的对象或<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition>对象 （在新的项目项类型的定义）。

3. 在事件处理程序，使用<xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs>和<xref:Microsoft.VisualStudio.SharePoint.DeploymentStepCompletedEventArgs>参数来获取有关部署步骤的信息。 例如，可以确定正在执行的部署步骤，并且是否正在该解决方案部署或收回。

## <a name="example"></a>示例
 下面的代码示例演示如何处理<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted>和<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepCompleted>列表实例项目项扩展中的事件。 此扩展将写入到的其他消息**输出**窗口时 Visual Studio 部署和收回解决方案的同时回收应用程序池。

 [!code-vb[SPExtensibility.ProjectSystemExtension.General#4](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/handledeploymentstepevents.vb#4)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#4](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/handledeploymentstepevents.cs#4)]

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>将扩展部署
 若要将扩展部署，创建[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (VSIX) 包的程序集和你想要将与该扩展一起分发的任何其他文件。 有关详细信息，请参阅[部署的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [演练：创建 SharePoint 项目的自定义部署步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)
- [如何：在部署或收回 SharePoint 项目时运行代码](../sharepoint/how-to-run-code-when-a-sharepoint-project-is-deployed-or-retracted.md)
