---
title: 部署 & 将 SharePoint 解决方案发布到本地 SharePoint 站点
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 59d4fe41565d0aaf0c52cae9434d4a576dc26baa
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016818"
---
# <a name="how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site"></a>如何：将 SharePoint 解决方案部署和发布到本地 SharePoint 站点
  你可以在开发计算机上将 SharePoint 解决方案部署或发布到本地 SharePoint 服务器。 部署过程会将 *.wsp*文件复制到 SharePoint 服务器，安装解决方案，然后激活功能。 发布过程仅将 *.wsp*文件复制到 SharePoint 服务器并安装该文件。 您必须手动激活它才能在 SharePoint 中启用它。

## <a name="to-deploy-a-sharepoint-solution-to-the-local-sharepoint-server"></a>将 SharePoint 解决方案部署到本地 SharePoint 服务器

1. 在**解决方案资源管理器**中，选择要部署的项目。

2. 在菜单栏上，依次选择 "**生成**"、"**部署解决方案**"。

     *.Wsp*文件在本地 SharePoint 服务器上创建并安装。 此外，还会激活这些功能。

## <a name="to-publish-a-sharepoint-solution-to-a-local-sharepoint-server"></a>将 SharePoint 解决方案发布到本地 SharePoint 服务器

1. 在**解决方案资源管理器**中，打开要发布的 SharePoint 项目的快捷菜单，然后选择 "**发布**"。

2. 在 "**发布**" 对话框中，选择 "**发布到文件系统**" 选项按钮。

3. 在 "**目标位置**" 文本框中，输入本地路径，然后选择 "**发布**" 按钮。

     发布进度将显示在 Visual Studio 的 "**输出**" 窗口中。 完成此过程后，解决方案（*.wsp*）文件将安装在本地 SharePoint 服务器上。 但是，还必须将其激活，才能在 SharePoint 中使用。 如果解决方案文件已存在，则会出现错误，并询问您是否要覆盖现有文件。 有关升级包的信息，请参阅[如何：在远程服务器上部署、发布和升级 SharePoint 解决方案](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)中有关升级远程包的部分。

## <a name="see-also"></a>另请参阅
- [如何：在远程服务器上部署、发布和升级 SharePoint 解决方案](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)
- [创建 SharePoint 解决方案包](../sharepoint/creating-sharepoint-solution-packages.md)
- [如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [如何：使用包设计器在包中添加和移除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
