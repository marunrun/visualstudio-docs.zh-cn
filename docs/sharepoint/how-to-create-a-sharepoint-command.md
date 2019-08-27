---
title: 如何：创建 SharePoint 命令 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: d804acd19d585bf9517ce9b8d771290a1f1c214a
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435459"
---
# <a name="how-to-create-a-sharepoint-command"></a>如何：创建 SharePoint 命令
  如果你想要在 SharePoint 工具扩展中使用服务器对象模型，则必须创建一个自定义*SharePoint 命令*来调用 API。 直接调入服务器对象模型的程序集中定义的 SharePoint 命令。

 有关用途的 SharePoint 命令的详细信息，请参阅[调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

### <a name="to-create-a-sharepoint-command"></a>若要创建 SharePoint 命令

1. 创建一个类库项目具有以下配置：

    - 面向.NET Framework 3.5。 有关选择的目标框架的详细信息，请参阅[如何：面向 .NET Framework 的某个版本](../ide/how-to-target-a-version-of-the-dotnet-framework.md)。

    - 面向 AnyCPU 或 x64 平台。 默认情况下，类库项目的目标平台为 AnyCPU。 有关选择目标平台的详细信息，请参阅[如何：将项目配置为面向平台](../ide/how-to-configure-projects-to-target-platforms.md)。

    > [!NOTE]
    > 不能定义 SharePoint 工具扩展，在同一项目中实现 SharePoint 命令，因为 SharePoint 命令针对.NET Framework 3.5 和 SharePoint 工具扩展目标[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]。 必须定义任何由你在一个单独的项目中的扩展的 SharePoint 命令。 有关详细信息，请参阅[部署的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio.SharePoint.Commands

    - Microsoft.SharePoint

3. 在项目中类中，创建定义您的 SharePoint 命令的方法。 该方法必须符合以下要求：

    - 它可以具有一个或两个参数。

         第一个参数必须是<xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext>对象。 此对象提供 Microsoft.SharePoint.SPSite 或 Microsoft.SharePoint.SPWeb 在其中执行此命令。 它还提供了<xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandLogger>对象，它可用于将消息写入**输出**窗口或**错误列表**Visual Studio 窗口中的。

         第二个参数可以是所选的类型，但此参数是可选的。 如果你需要将数据从 SharePoint 工具扩展插件传递到命令，可以向 SharePoint 命令添加此参数。

    - 它可以有一个返回值，但这是可选的。

    - 第二个参数和返回值必须是可序列化的 Windows Communication Foundation (WCF) 的类型。 有关详细信息，请参阅[类型支持的数据协定序列化程序](/dotnet/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer)并[使用 XmlSerializer 类](/dotnet/framework/wcf/feature-details/using-the-xmlserializer-class)。

    - 该方法可以具有任何可见性 (**公共**，**内部**，或**专用**)，它可以是静态或非静态。

4. 将应用<xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute>方法。 此属性指定该命令; 的唯一标识符此标识符不需要与方法名称匹配。

     从 SharePoint 工具扩展调用命令时，必须指定相同的唯一标识符。 有关详细信息，请参阅[如何：执行 SharePoint 命令](../sharepoint/how-to-execute-a-sharepoint-command.md)。

## <a name="example"></a>示例
 下面的代码示例演示了具有标识符的 SharePoint 命令`Contoso.Commands.UpgradeSolution`。 此命令使用服务器对象模型中的 Api 来升级到已部署的解决方案。

 [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#5](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/SharePointCommands/Commands.cs#5)]
 [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#5](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/sharepointcommands/commands.vb#5)]

 除了第一个隐式<xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext>参数，此命令还包含自定义字符串参数，其中包含正在升级到 SharePoint 站点的.wsp 文件的完整路径。 若要查看更大示例的上下文中此代码，请参阅[演练：创建 SharePoint 项目的自定义部署步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)。

## <a name="compiling-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint.Commands

- Microsoft.SharePoint

## <a name="deploying-the-command"></a>部署命令
 若要部署该命令，将命令程序集包含相同[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (*vsix*) 与使用该命令扩展插件程序集的包。 此外必须为 extension.vsixmanifest 文件中的命令程序集添加一个条目。 有关详细信息，请参阅[部署的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [如何：执行 SharePoint 命令](../sharepoint/how-to-execute-a-sharepoint-command.md)
- [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
