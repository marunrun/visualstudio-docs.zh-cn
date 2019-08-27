---
title: 部署和发布到本地 SharePoint 站点的 SharePoint 解决方案
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 3e68fc4e49311535169ab37a2332b443ba632fb5
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401452"
---
# <a name="how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site"></a>如何：部署和发布到本地 SharePoint 站点的 SharePoint 解决方案
  可以部署或在开发计算机上将 SharePoint 解决方案发布到本地 SharePoint 服务器。 部署进程副本 *.wsp*文件到 SharePoint 服务器，安装该解决方案，然后激活功能。 发布处理仅副本 *.wsp*到 SharePoint 服务器的文件并将其安装。 您必须手动激活它，以使它在 SharePoint 中。

## <a name="to-deploy-a-sharepoint-solution-to-the-local-sharepoint-server"></a>若要将 SharePoint 解决方案部署到本地 SharePoint 服务器

1. 在中**解决方案资源管理器**，选择你想要部署的项目。

2. 在菜单栏上依次选择**构建**，**部署解决方案**。

     *.Wsp*创建文件并将其安装在本地 SharePoint 服务器上。 此外，将激活功能。

## <a name="to-publish-a-sharepoint-solution-to-a-local-sharepoint-server"></a>若要将 SharePoint 解决方案发布到本地 SharePoint 服务器

1. 在中**解决方案资源管理器**，打开你想要发布，然后选择 SharePoint 项目的快捷菜单**发布**。

2. 在中**发布**对话框框中，选择**发布到文件系统**选项按钮。

3. 在中**目标位置**文本框中，输入本地路径，然后选择**发布**按钮。

     在 Visual Studio 中会显示发布进度**输出**窗口。 当完成该过程，该解决方案 ( *.wsp*) 文件安装在本地 SharePoint 服务器上。 但是，它仍必须激活要在 SharePoint 中使用。 如果解决方案文件已存在，错误出现，询问您是否要覆盖现有文件。 升级包的信息，请参阅部分在升级中的远程包[如何：部署、 发布和升级 SharePoint 解决方案的远程服务器上](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)。

## <a name="see-also"></a>请参阅
- [如何：部署、 发布和升级远程服务器上的 SharePoint 解决方案](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)
- [创建 SharePoint 解决方案包](../sharepoint/creating-sharepoint-solution-packages.md)
- [如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [如何：添加和删除使用包设计器的功能和包项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
