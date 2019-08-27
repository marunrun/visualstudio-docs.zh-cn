---
title: 发布页，项目设计器 （Office 开发）
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ProjectProperties.Publish.2007System
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- deploying applications [Office development in Visual Studio]
- publishing, Office solutions
- Property Pages dialog box, Publish [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 86d575b254209b547504ea6d746d03853990bfb4
ms.sourcegitcommit: 7eb2fb21805d92f085126f3a820ac274f2216b4e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2019
ms.locfileid: "67329001"
---
# <a name="publish-page-project-designer-office-development-in-visual-studio"></a>发布页，项目设计器 （在 Visual Studio 中的 Office 开发）
  “项目设计器”  的“发布”  页面用于针对部署配置属性。

 若要访问此页，请选择中的项目**解决方案资源管理器**，然后在**项目**菜单中，选择*Projectname* **属性**. 如果“发布”  页面未显示，请选择“发布”  选项卡。

> [!NOTE]
> 你也可以在“发布向导”  中设置发布位置。 有关详细信息，请参阅[如何：使用 ClickOnce 发布 Office 解决方案](https://msdn.microsoft.com/2b6c247e-bc04-4ce4-bb64-c4e79bb3d5b8)。

## <a name="uielement-list"></a>UIElement 列表
 **发布文件夹位置 （网站、 ftp 服务器或文件路径）** 所需。

 发布文件夹位置是 Visual Studio 将解决方案文件（例如清单、程序集和生成中的其他文件）复制到的目录。 你必须对此目录具有写权限。

 可选的位置包括本地计算机、UNC 文件共享或 HTTP/HTTPS 网站。 路径可以是本地 (*c:\foldername\publishfolder*)、 相对 (*发布\\* )，或完全限定的位置 ( *\\\servername\foldername*或 http://<em>servername/foldername</em>)。

 默认情况下，发布位置是 *http://localhost/projectname/* 如果您安装了 IIS，或*发布\\* 目录，如果您没有安装 IIS。

 **安装文件夹 URL**可选。

 安装文件夹 URL 是最终用户将从其中安装自定义项的目录。 这也是解决方案将用于检查更新的路径。 该路径可以与发布文件夹位置相同，但并非必要。

 可选的位置包括本地计算机、UNC 文件共享或 HTTP/HTTPS 网站。 路径可以是本地 (*c:\foldername\publishfolder*)、 相对 (*发布\\* )，或完全限定的位置 ( *\\\servername\foldername*或 http://<em>servername/foldername</em>)。 所有 HTTP/HTTPS 位置都必须使用 US-ASCII 字符创建。 不支持 Unicode 字符。

 如果设置了安装路径，则自定义项文件必须位于该位置，用户才能安装自定义项。 在知道最终部署位置的情况下，才应设置该位置。

 如果安装文件位于相对于文档或安装程序的位置（例如使用 CD 的时候），则将此框保留为空。

 此值可由管理员以后分配。 有关详细信息，请参阅[如何：更改 Office 解决方案的安装路径](https://msdn.microsoft.com/d0eaa07b-2d72-4902-899f-2f9fb165b8fd)。

 **先决条件**可以包含的安装程序或在安装过程中按需下载系统必备组件。

- **从组件供应商的网站上下载系统必备组件**:使用此选项将从 Microsoft 下载这些系统必备组件。

- **从与我的应用程序相同的位置下载系统必备组件**:使用此选项将打包到安装程序中的先决条件。 在安装程序中包含系统必备文件会增加解决方案的大小。

- **从以下位置下载系统必备组件**:使用此选项可为网页或网络共享上的另一安装程序单独向最终用户提供了系统必备组件。

  **更新**更新间隔决定解决方案检查更新的频率。 默认值为每七天检查一次。

  可以在每次加载文档级自定义项或 VSTO 外接程序时都检查更新，这样做可以使这些组件保持最新状态，但会影响启动性能。

  如果要使用 CD 或可移动驱动器进行部署，请将此选项设置为“从不检查更新”  。

  **选项 （描述）** 可以设置以下属性的发布选项：

- 发布语言：Office 解决方案的区域设置。

- 发布者名称：出现在“添加/删除程序”  或“程序和功能”  中的公司名称或开发人员名称。

- 产品名：出现在“添加/删除程序”  或“程序和功能”  中的 Office 解决方案名称。

- 支持 URL：可供最终用户与 Office 解决方案的技术支持人员联系的位置。

  **选项 （Office 设置）** 可以设置以下属性的发布选项：

- 解决方案名称：出现在 Office 应用程序中的 Office 解决方案名称。

- 描述：出现在 Office 应用程序中的 Office 解决方案的描述。

- VSTO 外接程序加载行为。

  - 启动时加载：指定 VSTO 外接程序在 Office 应用程序启动时加载。

  - 按需加载：指定 VSTO 外接程序在应用程序需要它时加载，例如当用户单击某个用到 VSTO 外接程序中的功能的 UI 元素时加载。

  **发布语言**此选项设置的语言的 Microsoft 软件许可条款，并在系统必备组件列表中包括的语言包。 它不会影响自定义项的语言。 安装程序中的语言取决于 Visual Studio 已安装的语言。

  有关如何更改详细信息**发布语言**，请参阅[如何：更改 ClickOnce 应用程序的发布语言](../deployment/how-to-change-the-publish-language-for-a-clickonce-application.md)。

  **发布版本**设置自定义项的版本号。 版本号更改时，会将应用程序作为更新发布。 在生成过程中，会针对每个版本创建一个新的文件夹，以免覆盖先前发布的版本。 发布版本的每个部分（“主要”  、“次要”  、“生成”  、“修订”  ）最多都可以包含五位数。

  **自动递增每个版本的修订号**可选。 选择该选项后（默认），版本号的“修订”  部分会在每次发布自定义项时递增 1。 这将导致自定义项作为更新发布。

  **立即发布**发布的应用程序使用当前设置。 等效于“发布向导”  中的“完成”  按钮。

## <a name="see-also"></a>请参阅

- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
- [使用 ClickOnce 部署 Office 解决方案](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [用于部署 office 解决方案必备组件](https://msdn.microsoft.com/9f672809-43a3-40a1-9057-397ce3b5126e)
