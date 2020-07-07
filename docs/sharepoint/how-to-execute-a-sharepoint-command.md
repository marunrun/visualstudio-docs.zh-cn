---
title: 如何：执行 SharePoint 命令 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands [SharePoint development in Visual Studio], executing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 789b77f3161b5fe566ea033060e8cab16cbaecc7
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016984"
---
# <a name="how-to-execute-a-sharepoint-command"></a>如何：执行 SharePoint 命令
  如果要在 SharePoint 工具扩展中使用服务器对象模型，则必须创建自定义*SharePoint 命令*以调用 API。 定义该命令并将其与 SharePoint 工具扩展一起部署后，扩展可以执行命令以调入 SharePoint 服务器对象模型。 若要执行该命令，请使用对象的 ExecuteCommand 方法之一 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> 。

 有关 SharePoint 命令用途的详细信息，请参阅[调入 sharepoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

### <a name="to-execute-a-sharepoint-command"></a>执行 SharePoint 命令

1. 在 SharePoint 工具扩展中获取一个 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> 对象。 获取对象的方式 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> 取决于要创建的扩展的类型：

    - 在 SharePoint 项目系统的扩展中，使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.SharePointConnection%2A> 属性。

         有关项目系统扩展的详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

    - 在**服务器资源管理器**的 " **SharePoint 连接**" 节点的扩展中，使用 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeContext.SharePointConnection%2A> 属性。 若要获取 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeContext> 对象，请使用 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.Context%2A> 属性。

         有关**服务器资源管理器**扩展的详细信息，请参阅[服务器资源管理器中的 "扩展 SharePoint 连接" 节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

    - 在不属于 SharePoint 工具扩展的代码中，如项目模板向导，使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.SharePointConnection%2A> 属性。

         有关检索项目服务的详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

2. 调用对象的 ExecuteCommand 方法之一 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> 。 将要执行的命令的名称传递给 ExecuteCommand 方法的第一个自变量。 如果你的命令具有自定义参数，请将该参数传递给 ExecuteCommand 方法的第二个参数。

     每个受支持的命令签名都有不同的 ExecuteCommand 重载。 下表列出了支持的签名以及要用于每个签名的重载。

    |命令签名|要使用的 ExecuteCommand 重载|
    |-----------------------|------------------------------------|
    |命令只包含默认 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 参数，没有返回值。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |命令只有默认 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 参数和返回值。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |命令有两个参数（默认 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 参数和自定义参数）和不返回值。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |命令有两个参数和一个返回值。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|

## <a name="example"></a>示例
 下面的代码示例演示如何使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A> 重载调用 `Contoso.Commands.UpgradeSolution` [如何：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)中所述的命令。

 [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#6](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/upgradestep.cs#6)]
 [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#6](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/upgradestep.vb#6)]

 `Execute`本示例中所示的方法是 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep.Execute%2A> <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep> 自定义部署步骤中接口的方法的实现。 若要在更大的示例上下文中查看此代码，请参阅[演练：为 SharePoint 项目创建自定义部署步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)。

 请注意以下有关对方法的调用的详细信息 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A> ：

- 第一个参数标识要调用的命令。 此字符串与传递给 <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> 命令定义上的值匹配。

- 第二个参数是要传递给命令的自定义第二个参数的值。 在这种情况下，它是要升级到 SharePoint 站点的 *.wsp*文件的完整路径。

- 此代码不会将隐式 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 参数传递给命令。 当你从 SharePoint 项目系统的扩展或**服务器资源管理器**中**sharepoint 连接**节点的扩展中调用命令时，此参数将自动传递到该命令。 在其他类型的解决方案中，如在实现接口的项目模板向导中 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> ，此参数为**null**。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用 VisualStudio 程序集。

## <a name="see-also"></a>另请参阅
- [调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [如何：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)
- [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
