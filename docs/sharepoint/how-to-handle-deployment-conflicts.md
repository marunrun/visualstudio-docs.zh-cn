---
title: 如何：处理部署冲突 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 62e7740915d341eee1bbf5e112c4f09297c98be1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62813794"
---
# <a name="how-to-handle-deployment-conflicts"></a>如何：处理部署冲突
  可以提供自己的代码来处理 SharePoint 项目项的部署冲突。 例如，可以确定是否当前项目项中的任何文件已存在于部署位置，并且当前的项目项部署之前，然后删除已部署的文件。 有关部署冲突的详细信息，请参阅[扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)。

### <a name="to-handle-a-deployment-conflict"></a>若要处理部署冲突

1. 创建项目项扩展、 项目扩展或新的项目项类型的定义。 有关详细信息，请参阅下列主题：

    - [如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

    - [如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

    - [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. 在扩展中，处理<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted>的事件<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType>（在项目项扩展或项目扩展） 的对象或<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition>对象 （在新的项目项类型的定义）。

3. 在事件处理程序，确定是否存在正在部署的项目项和适用于方案的条件的 SharePoint 站点上部署的解决方案之间的冲突。 可以使用<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemEventArgs.ProjectItem%2A>分析正在部署的项目项的事件自变量参数的属性，可以通过调用定义为用于此用途的 SharePoint 命令分析部署位置的文件。

     对于许多类型的冲突，可能首先想要确定执行的部署步骤。 您可以执行此操作通过使用<xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs.DeploymentStepInfo%2A>事件自变量参数的属性。 尽管通常最好在内置检测冲突<xref:Microsoft.VisualStudio.SharePoint.Deployment.DeploymentStepIds.AddSolution>部署步骤中，您可以检查冲突在任何部署步骤。

4. 如果存在冲突，使用<xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflictCollection.Add%2A>方法<xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs.Conflicts%2A>的事件参数以创建一个新属性<xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict>对象。 此对象表示部署冲突。 在调用<xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflictCollection.Add%2A>方法，还指定调用来解决冲突的方法。

## <a name="example"></a>示例
 下面的代码示例演示如何处理部署冲突列表定义项目项的项目项扩展中的基本过程。 若要处理不同类型的项目项的部署冲突，请将传递到不同的字符串<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>。 有关详细信息，请参阅[扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)。

 为简单起见，<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted>事件处理程序在此示例假定存在部署冲突 (也就是说，它始终将添加一个新<xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict>对象)，并`Resolve`方法仅返回**true**指示已解决冲突。 在实际方案中，你<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted>事件处理程序将首先确定当前的项目项中的文件和在部署位置的文件之间存在冲突，然后添加<xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict>仅对象是否存在冲突。 例如，可以使用`e.ProjectItem.Files`分析中的项目项，并且您的文件的事件处理程序中的属性可能会在调用分析部署位置的文件的 SharePoint 命令。 同样，在实际情况`Resolve`方法可能会调用 SharePoint 命令以解决 SharePoint 站点上的冲突。 有关创建 SharePoint 命令的详细信息，请参阅[如何：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)。

 [!code-vb[SPExtensibility.ProjectItemExtension.DeploymentConflict#1](../sharepoint/codesnippet/VisualBasic/deploymentconflict/extension/deploymentconflictextension.vb#1)]
 [!code-csharp[SPExtensibility.ProjectItemExtension.DeploymentConflict#1](../sharepoint/codesnippet/CSharp/deploymentconflict/extension/deploymentconflictextension.cs#1)]

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>将扩展部署
 若要将扩展部署，创建[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (VSIX) 包的程序集和你想要将与该扩展一起分发的任何其他文件。 有关详细信息，请参阅[部署的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)
- [如何：执行部署步骤时运行代码](../sharepoint/how-to-run-code-when-deployment-steps-are-executed.md)
- [如何：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)
