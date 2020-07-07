---
title: 如何：创建 SharePoint 命令 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 15ea7ff86e90bf7a474f9d64c30a9803e3e20bf5
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016215"
---
# <a name="how-to-create-a-sharepoint-command"></a>如何：创建 SharePoint 命令
  如果要在 SharePoint 工具扩展中使用服务器对象模型，则必须创建自定义*SharePoint 命令*以调用 API。 在可直接调入服务器对象模型的程序集中定义 SharePoint 命令。

 有关 SharePoint 命令用途的详细信息，请参阅[调入 sharepoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

### <a name="to-create-a-sharepoint-command"></a>创建 SharePoint 命令

1. 创建一个具有以下配置的类库项目：

    - 面向 .NET Framework 3.5。 有关选择目标框架的详细信息，请参阅[如何：面向某个版本的 .NET Framework](../ide/visual-studio-multi-targeting-overview.md)。

    - 面向 AnyCPU 或 x64 平台。 默认情况下，类库项目的目标平台是 AnyCPU。 有关选择目标平台的详细信息，请参阅[如何：配置项目以面向目标平台](../ide/how-to-configure-projects-to-target-platforms.md)。

    > [!NOTE]
    > 不能在定义 SharePoint 工具扩展的同一项目中实现 SharePoint 命令，因为 SharePoint 命令面向 .NET Framework 3.5 和 SharePoint 工具扩展 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 。 你必须在单独的项目中定义你的扩展所使用的任何 SharePoint 命令。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

2. 添加对下列程序集的引用：

    - VisualStudio 命令

    - Microsoft SharePoint

3. 在项目的类中，创建一个定义 SharePoint 命令的方法。 该方法必须符合以下准则：

    - 它可以有一个或两个参数。

         第一个参数必须是一个 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 对象。 此对象提供在其中执行命令的 Microsoft. SPSite 或 node.js。 它还提供一个 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandLogger> 对象，该对象可用于将消息写入到 "**输出**" 窗口或 Visual Studio 中的 "**错误列表**" 窗口。

         第二个参数可以是你选择的类型，但此参数是可选的。 如果需要将数据从 SharePoint 工具扩展传递到命令，则可以将此参数添加到 SharePoint 命令。

    - 它可以有返回值，但这是可选的。

    - 第二个参数和返回值必须是可以由 Windows Communication Foundation （WCF）序列化的类型。 有关详细信息，请参阅[数据协定序列化程序支持的类型](/dotnet/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer)和[使用 XmlSerializer 类](/dotnet/framework/wcf/feature-details/using-the-xmlserializer-class)。

    - 此方法可以具有任何可见性（**公共**、**内部**或**私有**），并且它可以为静态或非静态。

4. 将应用 <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> 到方法。 此属性指定该命令的唯一标识符;此标识符不必与方法名称匹配。

     从 SharePoint 工具扩展中调用命令时，必须指定相同的唯一标识符。 有关详细信息，请参阅[如何：执行 SharePoint 命令](../sharepoint/how-to-execute-a-sharepoint-command.md)。

## <a name="example"></a>示例
 下面的代码示例演示一个具有标识符的 SharePoint 命令 `Contoso.Commands.UpgradeSolution` 。 此命令使用服务器对象模型中的 Api 升级到已部署的解决方案。

 [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#5](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/SharePointCommands/Commands.cs#5)]
 [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#5](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/sharepointcommands/commands.vb#5)]

 除了隐式的第一个 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 参数外，此命令还具有一个自定义字符串参数，该参数包含正在升级到 SharePoint 站点的 .wsp 文件的完整路径。 若要在更大的示例上下文中查看此代码，请参阅[演练：为 SharePoint 项目创建自定义部署步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)。

## <a name="compiling-the-code"></a>编译代码
 此示例需要引用以下程序集：

- VisualStudio 命令

- Microsoft SharePoint

## <a name="deploying-the-command"></a>部署命令
 若要部署此命令，请将命令程序集包含在使用 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 命令的扩展程序集所在的同一扩展（*vsix*）包中。 还必须在 source.extension.vsixmanifest 文件中为命令程序集添加一个项。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [如何：执行 SharePoint 命令](../sharepoint/how-to-execute-a-sharepoint-command.md)
- [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
