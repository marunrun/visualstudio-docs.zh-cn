---
title: 如何：执行 SharePoint 命令 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 6f5c285e71179c5dd59fad0357dbf71ee4b32f9d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62813884"
---
# <a name="how-to-execute-a-sharepoint-command"></a>如何：执行 SharePoint 命令
  如果你想要在 SharePoint 工具扩展中使用服务器对象模型，则必须创建一个自定义*SharePoint 命令*来调用 API。 定义该命令并将其部署与 SharePoint 工具扩展插件后，您的扩展插件可以执行命令来调入 SharePoint 服务器对象模型。 若要执行此命令，使用 ExecuteCommand 方法之一<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection>对象。

 有关用途的 SharePoint 命令的详细信息，请参阅[调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

### <a name="to-execute-a-sharepoint-command"></a>若要执行 SharePoint 命令

1. 在 SharePoint 工具扩展中，获取<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection>对象。 您获得的方式<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection>对象依赖于要创建的扩展的类型：

    - 在 SharePoint 项目系统的扩展，使用<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.SharePointConnection%2A>属性。

         项目系统扩展的详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

    - 中的扩展**SharePoint 连接**中的节点**服务器资源管理器**，使用<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeContext.SharePointConnection%2A>属性。 若要获取<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeContext>对象，请使用<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.Context%2A>属性。

         有关详细信息**服务器资源管理器**扩展，请参阅[扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

    - 在代码中的不是 SharePoint 工具，如项目模板向导中，扩展的一部分使用<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.SharePointConnection%2A>属性。

         检索项目服务的详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

2. 调用 ExecuteCommand 方法之一<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection>对象。 请传递想要执行到 ExecuteCommand 方法的第一个参数的命令的名称。 如果您的命令有自定义参数，则将该参数传递给 ExecuteCommand 方法的第二个参数。

     没有为每个受支持的命令签名的不同 ExecuteCommand 重载。 下表列出了支持的签名以及哪一个重载用于每个签名。

    |命令签名|若要使用的 ExecuteCommand 重载|
    |-----------------------|------------------------------------|
    |该命令仅具有默认<xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext>参数和没有返回值。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |该命令仅具有默认<xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext>参数和返回值。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |该命令具有两个参数 (默认值<xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext>参数和自定义参数)，没有返回值。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |该命令具有两个参数和返回值。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|

## <a name="example"></a>示例
 下面的代码示例演示如何使用<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>重载来调用`Contoso.Commands.UpgradeSolution`中所述的命令[如何：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)。

 [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#6](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/upgradestep.cs#6)]
 [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#6](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/upgradestep.vb#6)]

 `Execute`在此示例中所示的方法是实现<xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep.Execute%2A>方法的<xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep>接口中的自定义部署步骤。 若要查看更大示例的上下文中此代码，请参阅[演练：创建 SharePoint 项目的自定义部署步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)。

 请注意以下有关调用的详细信息<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>方法：

- 第一个参数标识你想要调用的命令。 此字符串匹配的值传递给<xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute>上的命令定义。

- 第二个参数是你想要传递给命令的自定义的第二个参数的值。 在这种情况下，它是完整路径 *.wsp*正在升级到 SharePoint 站点的文件。

- 该代码不会通过隐式<xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext>命令参数。 此参数传递到该命令会自动从 SharePoint 项目系统的扩展或扩展的调用命令时**SharePoint 连接**中的节点**服务器资源管理器**. 在其他类型的解决方案，例如实现的项目模板向导<xref:Microsoft.VisualStudio.TemplateWizard.IWizard>接口，此参数是**null**。

## <a name="compile-the-code"></a>编译代码
 此示例需要 Microsoft.VisualStudio.SharePoint 程序集的引用。

## <a name="see-also"></a>请参阅
- [调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [如何：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)
- [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
