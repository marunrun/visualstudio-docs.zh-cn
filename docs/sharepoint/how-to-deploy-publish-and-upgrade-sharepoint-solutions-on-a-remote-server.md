---
title: 部署、 发布和远程升级 SharePoint 解决方案
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- remote deployment [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, remote deployment
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c8e9c46a9acaf8c70fa434514785276f9ba343d4
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401449"
---
# <a name="how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server"></a>如何：部署、 发布和升级远程服务器上的 SharePoint 解决方案
  除了对本地系统中部署 SharePoint 解决方案，可以将沙盒 SharePoint 解决方案发布到远程站点或本地 SharePoint 站点中。 远程发布进程副本 *.wsp*文件到 SharePoint 服务器，安装解决方案，然后再启用您激活解决方案。 对其进行更改之后，你还可以升级远程 SharePoint 解决方案安装。

## <a name="to-publish-a-sandboxed-sharepoint-solution-to-a-remote-sharepoint-server"></a>若要将沙盒 SharePoint 解决方案发布到远程 SharePoint 服务器

1. 在中**解决方案资源管理器**，打开你想要发布，然后选择沙盒 SharePoint 项目的快捷菜单**发布**。

2. 在中**发布**对话框框中，选择**发布到 SharePoint 站点**选项按钮，然后输入的 URL 为联机的发布站点，如： `https://mytestsite.sharepoint.microsoftonline.com`。

3. 选择**发布后在浏览器中打开解决方案库页**选项按钮以查看中解决方案的列表**解决方案库**发布后的页。

4. 选择**发布**按钮。

5. 如果需要进行用户身份验证，登录到远程服务器。

     在 Visual Studio 中会显示发布进度**输出**窗口。 当完成该过程，该解决方案 ( *.wsp*) 文件安装在远程 SharePoint 服务器上。 但是，它仍必须激活才能在 SharePoint 中使用。

6. 上**解决方案库**页上，选择 SharePoint 应用程序，然后在功能区中选择**激活**按钮。

7. 在中**激活解决方案**对话框中，在功能区中，选择**激活**按钮再次。

     **状态**上的列**解决方案库**页指示应用程序处于活动状态。

## <a name="to-upgrade-a-sandboxed-sharepoint-solution-on-a-remote-sharepoint-server"></a>若要升级远程 SharePoint 服务器上的沙盒 SharePoint 解决方案
 如果远程服务器上已发布沙盒 SharePoint 解决方案，下面的过程，您可以将其升级到中的应用程序进行更改之后[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

1. 重命名中的 SharePoint 包[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。 若要执行此操作，在**解决方案资源管理器**中打开包。 它显示在**包资源管理器**。

2. 在中**包资源管理器**，在**名称**框中，将包名称更改为唯一名称。

3. 保存项目。

4. 在中**解决方案资源管理器**，打开项目的快捷菜单，然后选择**发布**。

5. 在中**发布**对话框框中，选择**发布到 SharePoint 站点**选项按钮，然后，如果缺少该解决方案的保存位置的远程服务器的 URL，则输入它。

6. 选择**发布后在浏览器中打开解决方案库页**选项按钮以查看中解决方案的列表**解决方案库**发布后的页。

7. 选择**发布**按钮。

8. 如果需要进行用户身份验证，登录到远程服务器。

     如果你登录到远程服务器最近，可能不需要身份验证。

     如果在 SharePoint 服务器上仍存在具有相同名称的应用程序的较旧版本，则会出错，SharePoint 服务器上已存在具有相同名称的包。 为唯一的名称在发布前，必须重命名包。

9. 在 SharePoint 中，选择新的应用程序，然后，在功能区中选择**升级**按钮。

10. 在中**升级解决方案**对话框中，在功能区中，选择**升级**按钮再次。 **状态**上的列**解决方案库**页现在应指示应用程序处于活动状态。

     停用旧版本的解决方案，从旧的解决方案中，保留数据升级解决方案的新版本，而在 SharePoint 中激活新的解决方案。

## <a name="see-also"></a>请参阅
- [如何：部署和发布到本地 SharePoint 站点的 SharePoint 解决方案](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)
- [创建 SharePoint 解决方案包](../sharepoint/creating-sharepoint-solution-packages.md)
- [如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [如何：添加和删除使用包设计器的功能和包项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
