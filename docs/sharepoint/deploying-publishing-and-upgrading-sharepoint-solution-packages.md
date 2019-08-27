---
title: 部署、 发布和升级 SharePoint 解决方案包
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
ms.openlocfilehash: 7c41b36766e112dc86bd15c7a2bec48633c35b57
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66402045"
---
# <a name="deploy-publish-and-upgrade-sharepoint-solution-packages"></a>部署、 发布和升级 SharePoint 解决方案包
  在开发 Visual Studio 中的 SharePoint 解决方案后，可以将其包 (.wsp) 文件部署到本地 SharePoint 服务器或将其发布到远程或本地 SharePoint 服务器。 如果你部署文件，您可以自定义部署的包文件 (.wsp) 的方式。

> [!NOTE]
> 目前，仅为沙盒解决方案可以发布到远程 SharePoint 服务器。 有关详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

## <a name="deploy-publish-and-upgrade"></a>部署、 发布和升级
 *部署*是指将复制到本地主机从 Visual Studio 中的 SharePoint 项目生成 SharePoint 解决方案文件。 在已部署的解决方案中，可以配置的部署步骤，如回收 Internet 信息服务 (IIS) 池，在部署后，激活解决方案和等等。 若要部署，请使用**部署**命令**生成**菜单。 有关详细信息，请参阅[如何：编辑 SharePoint 部署配置](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)和[如何：部署和发布到本地 SharePoint 站点的 SharePoint 解决方案](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)。

 *发布*指沙盒的 SharePoint 解决方案文件上传到远程 SharePoint 站点; 即，另一个系统上的站点。 此外可以将 SharePoint 沙盒解决方案文件发布到本地 SharePoint 站点，但无论发布到的站点是本地或远程的不能配置其部署步骤。

 *升级*指的是更新现有的远程或本地已发布的 SharePoint 解决方案。 对 Visual Studio 中的 SharePoint 解决方案的任何更改后，更改解决方案的包文件的名称、 重新发布该解决方案，并后成功重新发布，然后升级该解决方案。 如果重新发布本地已发布的解决方案时，可以覆盖现有的解决方案文件。

## <a name="deploy-packages"></a>部署包
 您可以用于测试和调试在开发计算机上将包文件部署到 SharePoint 服务器中。 此外可以创建可以通过选择安装在另一台计算机的包文件**发布到文件系统**中的选项按钮**发布**对话框。 创建包并将其复制到指定的本地文件路径。 若要将 SharePoint 解决方案部署到本地服务器，请使用**部署**命令**生成**菜单。 有关详细信息，请参阅[如何：部署和发布到本地 SharePoint 站点的 SharePoint 解决方案](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)。

 若要了解如何部署列表定义、 添加事件接收器，和使用的功能设计器和包设计器，请参阅[演练：部署项目任务列表定义](../sharepoint/walkthrough-deploying-a-project-task-list-definition.md)。

## <a name="customize-the-deployment-process"></a>自定义部署过程
 下表显示了在调试和部署 SharePoint 解决方案时可以使用两个部署配置。

|部署配置|描述|
|------------------------------|-----------------|
|默认|默认部署配置。 执行以下部署步骤：<br /><br /> 1.运行预先部署命令。<br />2.回收 IIS 应用程序池。<br />3.收回解决方案。<br />4.将解决方案添加。<br />5.激活功能。<br />6.运行后期部署命令。<br /><br /> 卸载包时，执行以下的收回步骤。<br /><br /> 1.回收 IIS 应用程序池。<br />2.收回解决方案。|
|无激活|此部署配置为默认配置中，运行相同的步骤，但将跳过激活步骤。|

 可以创建自己的部署配置，以完成一个步骤或更改的部署过程中的步骤顺序。 有关详细信息，请参阅[如何：编辑 SharePoint 部署配置](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)。

 此外可以添加要运行部署之前和之后的命令。 有关详细信息，请参阅[如何：设置 SharePoint 部署命令](../sharepoint/how-to-set-sharepoint-deployment-commands.md)。

## <a name="publish-packages-to-a-remote-or-local-server"></a>将包发布到远程或本地服务器
 若要将沙盒 SharePoint 解决方案发布到远程服务器，在菜单栏上，选择**构建**，**发布**，然后在**发布**对话框框中，选择**发布到 SharePoint 站点**选项按钮，提供远程服务器的 URL，如 **https://someremoteserver.sharepoint.microsoftonline.com** 。

 若要在中发布到本地服务器的 SharePoint 解决方案**发布**对话框框中，选择**发布到文件系统**选项按钮，提供本地系统路径。

 一种解决方案已成功将发布到 SharePoint 后，解决方案将出现在**解决方案库**可以激活。 有关详细信息，请参阅[如何：部署、 发布和升级 SharePoint 解决方案的远程服务器上](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)。

### <a name="upgrade-published-packages"></a>升级已发布的包
 如果发布后，可对 Visual Studio 中的 SharePoint 项目中进行任何更改，必须升级已发布的包要包括这些更改。 若要成功升级，包必须具有唯一名称。 如果具有相同名称的包发现-这会更新现有的应用程序时的 SharePoint 站点上的错误警报到的文件的名称冲突，并允许您重命名包。 后重新发布，新的包在 SharePoint 站点上会显示，就可以升级。 升级的包通过使用更低的包中的数据来更新该解决方案，然后激活 SharePoint 中的解决方案。 有关详细信息，请参阅[如何：部署、 发布和升级 SharePoint 解决方案的远程服务器上](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)。

## <a name="see-also"></a>请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
