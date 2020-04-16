---
title: 部署、发布、&升级 SharePoint 解决方案包
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
ms.openlocfilehash: d8e55b01173e749395f60d189366a08907bdaccd
ms.sourcegitcommit: 7b60e81414a82c6d34f6de1a1f56115c9cd26943
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81444965"
---
# <a name="deploy-publish-and-upgrade-sharepoint-solution-packages"></a>部署、发布和升级 SharePoint 解决方案包
  在 Visual Studio 中开发 SharePoint 解决方案后，可以将其包 （.wsp） 文件部署到本地 SharePoint 服务器，也可以将其发布到远程或本地 SharePoint 服务器。 如果部署这些文件，则可以自定义包文件的部署方式。

> [!NOTE]
> 目前，只能将沙盒解决方案发布到远程 SharePoint 服务器。 有关详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

## <a name="deploy-publish-and-upgrade"></a>部署、发布和升级
 *部署*是指将从 Visual Studio 中的 SharePoint 项目生成的 SharePoint 解决方案文件复制到本地主机。 在已部署的解决方案中，可以配置部署步骤，例如回收 Internet 信息服务 （IIS） 池、部署后激活解决方案等。 要进行部署，请使用 **"生成**"菜单上的 **"部署"** 命令。 有关详细信息，请参阅[如何：编辑 SharePoint 部署配置](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)以及如何[：将 SharePoint 解决方案部署到本地 SharePoint 站点并将其发布到](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)。

 *发布*是指将沙盒的 SharePoint 解决方案文件上载到远程 SharePoint 站点;即位于另一个系统上的站点。 您还可以将 SharePoint 沙盒解决方案文件发布到本地 SharePoint 站点，但无论发布到站点是本地站点还是远程站点，您都无法配置其部署步骤。

 *升级*是指更新现有的远程或本地发布的 SharePoint 解决方案。 对 Visual Studio 中的 SharePoint 解决方案进行任何更改后，可以更改解决方案的包文件名，重新发布解决方案，然后在成功重新发布解决方案后升级解决方案。 如果重新发布本地发布的解决方案，则可以覆盖现有解决方案文件。

## <a name="deploy-packages"></a>部署包
 您可以将包文件部署到开发计算机上的 SharePoint 服务器以进行测试和调试。 您还可以通过"**发布到文件系统"** 对话框中的"发布到文件系统"选项按钮创建可以在另一台计算机上安装的包文件。 **Publish** 将创建包并将其复制到指定的本地文件路径。 要将 SharePoint 解决方案部署到本地服务器，请使用 **"生成**"菜单上的 **"部署"** 命令。 有关详细信息，请参阅[如何：将 SharePoint 解决方案部署到本地 SharePoint 站点并将其发布到](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)。

 要了解如何部署列表定义、添加事件接收器以及使用功能设计器和包设计器，请参阅[演练：部署项目任务列表定义](../sharepoint/walkthrough-deploying-a-project-task-list-definition.md)。

## <a name="customize-the-deployment-process"></a>自定义部署过程
 下表显示了在调试和部署 SharePoint 解决方案时可以使用的两种部署配置。

|部署配置|说明|
|------------------------------|-----------------|
|默认|默认部署配置。 执行以下部署步骤：<br /><br /> 1. 运行部署前命令。<br />2. 回收 IIS 应用程序池。<br />3. 缩回溶液。<br />4. 添加解决方案。<br />5. 激活功能。<br />6. 运行部署后命令。<br /><br /> 卸载包时，将执行以下撤回步骤。<br /><br /> 1. 回收 IIS 应用程序池。<br />2. 缩回溶液。|
|无激活|此部署配置运行的步骤与默认配置相同，但跳过激活步骤。|

 您可以创建自己的部署配置以完成单个步骤或更改部署过程中步骤的顺序。 有关详细信息，请参阅[如何：编辑 SharePoint 部署配置](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)。

 您还可以添加要在部署之前和之后运行的命令。 有关详细信息，请参阅[如何：设置 SharePoint 部署命令](../sharepoint/how-to-set-sharepoint-deployment-commands.md)。

## <a name="publish-packages-to-a-remote-or-local-server"></a>将包发布到远程或本地服务器
 要将沙盒的 SharePoint 解决方案发布到远程服务器，请选择菜单栏上的 **"生成**"、"**发布**"，然后在 **"发布"** 对话框中选择"**发布到 SharePoint 站点**"选项按钮，提供远程服务器的 URL，如`https://someremoteserver.sharepoint.microsoftonline.com`。

 要将 SharePoint 解决方案发布到本地服务器，请在 **"发布"** 对话框中选择"**发布到文件系统**"选项按钮，提供本地系统路径。

 解决方案成功发布到 SharePoint 后，该解决方案将显示在**解决方案库中**，您可以在其中激活它。 有关详细信息，请参阅[如何：在远程服务器上部署、发布和升级 SharePoint 解决方案](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)。

### <a name="upgrade-published-packages"></a>升级已发布的软件包
 如果在 Visual Studio 中对 SharePoint 项目进行任何更改，则必须升级已发布的包以包括更改。 要成功升级，包必须具有唯一名称。 如果在 SharePoint 站点上找到具有相同名称的包（在更新现有应用程序时可能发生）错误会提醒您文件名冲突，并允许您重命名包。 重新发布后，新包将显示在 SharePoint 网站上，可以升级。 升级的包使用旧包中的数据更新解决方案，然后在 SharePoint 中激活解决方案。 有关详细信息，请参阅[如何：在远程服务器上部署、发布和升级 SharePoint 解决方案](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)。

## <a name="see-also"></a>请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
