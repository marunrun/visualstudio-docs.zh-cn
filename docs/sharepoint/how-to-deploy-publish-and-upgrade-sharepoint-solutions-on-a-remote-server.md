---
title: 远程部署、发布、& 升级 SharePoint 解决方案
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: f05f42f8aed35696b962e71a5fce86c2956b3661
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86016800"
---
# <a name="how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server"></a>如何：在远程服务器上部署、发布和升级 SharePoint 解决方案
  除了将 SharePoint 解决方案部署到本地系统以外，还可以将沙盒 SharePoint 解决方案发布到远程站点或本地 SharePoint 站点。 远程发布过程会将 *.wsp* 文件复制到 SharePoint 服务器，安装解决方案，并使您能够激活解决方案。 你还可以在对其进行更改之后升级远程 SharePoint 解决方案安装。

## <a name="to-publish-a-sandboxed-sharepoint-solution-to-a-remote-sharepoint-server"></a>将沙盒 SharePoint 解决方案发布到远程 SharePoint 服务器

1. 在 **解决方案资源管理器**中，打开要发布的沙盒 SharePoint 项目的快捷菜单，然后选择 " **发布**"。

2. 在 " **发布** " 对话框中，选择 " **发布到 SharePoint 站点** " 选项按钮，然后输入联机发布网站的 URL，例如： `https://mytestsite.sharepoint.microsoftonline.com` 。

3. 在发布后，选择 "在 **发布后浏览器中打开解决方案库" 页** ，以便在 " **解决方案库** " 页中查看解决方案列表。

4. 选择 **“发布”** 按钮。

5. 如果需要用户身份验证，请登录到远程服务器。

     发布进度将显示在 Visual Studio 的 " **输出** " 窗口中。 完成此过程后，将在远程 SharePoint 服务器上安装解决方案 (*.wsp*) 文件。 但是，它仍必须先激活，然后才能在 SharePoint 中使用。

6. 在 " **解决方案库** " 页上，选择 "SharePoint" 应用程序，然后在功能区上，选择 " **激活** " 按钮。

7. 在 " **激活解决方案** " 对话框的功能区中，再次选择 " **激活** " 按钮。

     "**解决方案库**" 页上的 "**状态**" 列指示该应用程序处于活动状态。

## <a name="to-upgrade-a-sandboxed-sharepoint-solution-on-a-remote-sharepoint-server"></a>在远程 SharePoint 服务器上升级沙盒 SharePoint 解决方案
 如果已在远程服务器上发布沙盒 SharePoint 解决方案，则可以使用以下过程在中对应用程序进行更改后进行升级 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

1. 重命名中的 SharePoint 包 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 为此，请在 **解决方案资源管理器** 打开包。 它将出现在 **包资源管理器**中。

2. 在 " **包资源管理器**" 的 " **名称** " 框中，将包名称更改为唯一名称。

3. 保存项目。

4. 在 **解决方案资源管理器**中，打开项目的快捷菜单，然后选择 " **发布**"。

5. 在 " **发布** " 对话框中，选择 " **发布到 SharePoint 站点** " 选项按钮，然后，如果保存解决方案的远程服务器的 URL 丢失，请输入该 URL。

6. 在发布后，选择 "在 **发布后浏览器中打开解决方案库" 页** ，以便在 " **解决方案库** " 页中查看解决方案列表。

7. 选择 **“发布”** 按钮。

8. 如果需要用户身份验证，请登录到远程服务器。

     如果最近登录到远程服务器，则可能不需要进行身份验证。

     如果 SharePoint 服务器上仍然存在具有相同名称的较旧版本的应用程序，您将收到一个错误，指出 SharePoint 服务器上已存在同名的包。 在发布之前，必须先将包重命名为唯一名称。

9. 选择 SharePoint 中的新应用程序，然后在功能区上，选择 " **升级** " 按钮。

10. 在 " **升级解决方案** " 对话框的功能区中，再次选择 " **升级** " 按钮。 现在，"**解决方案库**" 页上的 "**状态**" 列指示该应用程序处于活动状态。

     旧版本的解决方案将被停用，新版本的解决方案将通过旧解决方案中保留的数据进行升级，并在 SharePoint 中激活新解决方案。

## <a name="see-also"></a>另请参阅
- [如何：将 SharePoint 解决方案部署和发布到本地 SharePoint 站点](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)
- [创建 SharePoint 解决方案包](../sharepoint/creating-sharepoint-solution-packages.md)
- [如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [如何：使用包设计器在包中添加和移除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
