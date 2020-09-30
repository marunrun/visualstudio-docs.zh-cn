---
title: 部署、发布、& 升级 SharePoint 解决方案包
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.SharePointProjectPropertyTab
- VS.SharePointTools.Project.Publishing
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 574712b870256fa7422e64a3c29ae8733f4c2251
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91583874"
---
# <a name="deploy-publish-and-upgrade-sharepoint-solution-packages"></a>部署、发布和升级 SharePoint 解决方案包
  在 Visual Studio 中开发 SharePoint 解决方案后，可以将其包 ( .wsp) 文件部署到本地 SharePoint 服务器，或者将其发布到远程或本地 SharePoint 服务器。 如果部署这些文件，可以自定义包文件 ( 的部署) 的部署方式。

> [!NOTE]
> 目前，只有沙盒解决方案才能发布到远程 SharePoint 服务器。 有关详细信息，请参阅 [沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

## <a name="deploy-publish-and-upgrade"></a>部署、发布和升级
 *部署* 是指将从 Visual Studio 中的 sharepoint 项目生成的 sharepoint 解决方案文件复制到本地主机。 在已部署的解决方案中，可以配置部署步骤，如将 Internet Information Services 回收 (IIS) 池、部署之后激活解决方案等。 若要部署，请使用 "**生成**" 菜单上的 "**部署**" 命令。 有关详细信息，请参阅 [如何：编辑 sharepoint 部署配置](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md) 和 [如何：将 sharepoint 解决方案部署和发布到本地 SharePoint 站点](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)。

 *发布* 是指将沙盒 SharePoint 解决方案文件上传到远程 SharePoint 站点;也就是说，位于另一个系统上的站点。 您还可以将 SharePoint 沙盒解决方案文件发布到本地 SharePoint 站点，但不管发布到本地还是远程站点，都不能配置其部署步骤。

 *升级* 是指更新现有的远程或本地发布的 SharePoint 解决方案。 在 Visual Studio 中对 SharePoint 解决方案进行任何更改后，更改解决方案的包文件名，重新发布解决方案，然后在成功重新发布后升级解决方案。 如果重新发布本地发布的解决方案，则可以覆盖现有解决方案文件。

## <a name="deploy-packages"></a>部署包
 你可以将包文件部署到开发计算机上的 SharePoint server，以便进行测试和调试。 还可以通过在 "**发布**" 对话框中选择 "**发布到文件系统**" 选项按钮，创建可以安装在另一台计算机上的包文件。 创建包并将其复制到指定的本地文件路径。 若要将 SharePoint 解决方案部署到本地服务器，请使用 "**生成**" 菜单上的 "**部署**" 命令。 有关详细信息，请参阅 [如何：将 SharePoint 解决方案部署和发布到本地 sharepoint 站点](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)。

 若要了解如何部署列表定义、添加事件接收器以及使用功能设计器和包设计器，请参阅 [演练：部署项目任务列表定义](../sharepoint/walkthrough-deploying-a-project-task-list-definition.md)。

## <a name="customize-the-deployment-process"></a>自定义部署过程
 下表显示了在调试和部署 SharePoint 解决方案时可以使用的两个部署配置。

|部署配置|说明|
|------------------------------|-----------------|
|默认|默认的部署配置。 执行以下部署步骤：<br /><br /> 1. 运行预先部署命令。<br />2. 回收 IIS 应用程序池。<br />3. 收回解决方案。<br />4. 添加解决方案。<br />5. 激活功能。<br />6. 运行后期部署命令。<br /><br /> 卸载包时，将执行以下收回步骤。<br /><br /> 1. 回收 IIS 应用程序池。<br />2. 收回解决方案。|
|无激活|此部署配置与默认配置运行相同的步骤，但会跳过激活步骤。|

 你可以创建自己的部署配置来完成单个步骤或更改部署过程中的步骤顺序。 有关详细信息，请参阅[如何：编辑 SharePoint 部署配置](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)。

 你还可以添加在部署之前和之后运行的命令。 有关详细信息，请参阅 [如何：设置 SharePoint 部署命令](../sharepoint/how-to-set-sharepoint-deployment-commands.md)。

## <a name="publish-packages-to-a-remote-or-local-server"></a>将包发布到远程或本地服务器
 若要将沙盒 SharePoint 解决方案发布到远程服务器，请在菜单栏上，依次选择 " **生成**"、" **发布**"，然后在 " **发布** " 对话框中，选择 " **发布到 SharePoint 站点** " 选项按钮，提供远程服务器的 URL，例如 `https://someremoteserver.sharepoint.microsoftonline.com` 。

 若要向本地服务器发布 SharePoint 解决方案，请在 " **发布** " 对话框中，选择 " **发布到文件系统** " 选项按钮，并提供本地系统路径。

 解决方案成功发布到 SharePoint 后，解决方案将显示在 **解决方案库** 中，您可以在其中激活解决方案。 有关详细信息，请参阅 [如何：在远程服务器上部署、发布和升级 SharePoint 解决方案](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)。

### <a name="upgrade-published-packages"></a>升级发布的包
 如果你在发布 Visual Studio 中的 SharePoint 项目后对其进行任何更改，则必须升级已发布的包以包含这些更改。 若要成功升级，包必须具有唯一的名称。 如果在 SharePoint 站点上找到具有相同名称的包（在更新现有应用程序时可能会发生此错误），则会出现文件名冲突，并允许您重命名此包。 重新发布后，新的包将显示在 SharePoint 站点上并可进行升级。 升级的包使用较旧包中的数据更新解决方案，然后在 SharePoint 中激活解决方案。 有关详细信息，请参阅 [如何：在远程服务器上部署、发布和升级 SharePoint 解决方案](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)。

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
