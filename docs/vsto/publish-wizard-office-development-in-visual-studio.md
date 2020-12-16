---
title: '发布向导 (Visual Studio 中的 Office 开发) '
description: 了解如何使用发布向导将解决方案文件复制到指定位置、创建清单文件，以及在 Visual Studio 中创建安装程序。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ProjectProperties.PublishWizard
- VST.PublishWizard.Publish.2007System
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ClickOnce deployment [Office development in Visual Studio], Publish Wizard
- deploying applications [Office development in Visual Studio], Publish Wizard
- Office applications [Office development in Visual Studio], Publish Wizard
- Publish Wizard, Office solutions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 25821a0f245f2f0ed30fcbfb10137a772dd0dd01
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97528015"
---
# <a name="publish-wizard-office-development-in-visual-studio"></a>发布向导 (Visual Studio 中的 Office 开发) 
  使用 **发布向导** 将解决方案文件复制到指定位置、创建清单文件并创建安装程序。

 若要访问此向导，请在 "**生成**" 菜单上选择 "**发布***解决方案名称*"。 您还可以从 **解决方案资源管理器** 访问 **发布向导**。 打开项目节点的快捷菜单，然后选择 " **发布**"。

 以下各节介绍向导的一页。

## <a name="where-do-you-want-to-publish-the-application"></a>要在何处发布应用程序？
 **指定发布此应用程序的位置** 必填。 发布位置是 **发布向导** 将解决方案文件（例如清单、程序集、临时证书和生成中的其他文件）复制到的目录。 你必须对此目录具有写权限。

 键入作为磁盘路径、文件共享、FTP 站点或网站 URL 的位置，或单击 " **浏览** " 按钮浏览到该位置。 路径可以采用以下格式：

- 标准 Windows 格式的相对路径或绝对路径，例如 *C:\Deploy\MyApplication* 或 *\MyApplication*。

- 通用命名约定 (UNC) 路径，例如 *\\ \ServerName\MyApplication \\*。

- 网站的 URL，例如 `http://www.contoso.com/MyApplication` 。

  默认情况下，如果安装了 IIS，则发布位置为; *http://localhost/projectname/* 如果未安装 iis，则为发布目录。

> [!NOTE]
> 如果目标计算机运行的是 Windows Vista，则有更多注意事项。 只有 Windows Vista 计算机上的管理员才能使用本地发布选项。 此外，无论是否安装了 IIS，默认位置始终为 *发布 \\* 目录。

## <a name="what-is-the-default-installation-path-on-end-user-computers"></a>最终用户计算机上的默认安装路径是什么？
 安装路径是可选的。 以后可以根据需要设置安装路径。 有关详细信息，请参阅 [如何：更改 Office 解决方案的安装路径](/previous-versions/bb608626(v=vs.110))。

 安装路径是最终用户将从其中安装自定义项的目录。 这也是解决方案将用于检查更新的路径。 **发布向导** 不会将解决方案部署到此位置，除非该路径与您在前一页上的 "**指定发布此应用程序的位置**" 框中输入的路径相同。

 **从** 网站指定最终用户将用于安装解决方案的 URL。

 **从 UNC 路径或文件共享** 指定最终用户安装解决方案时将遵循的 UNC 路径。

 **从 cd-rom 或 dvd-rom** 此选项不需要安装路径。

 Visual Studio 不会刻录 CD 或 DVD。 必须手动将输出复制到 CD 或 DVD。

## <a name="see-also"></a>另请参阅
- [使用 ClickOnce 部署 Office 解决方案](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [发布页，项目设计器 &#40;Visual Studio 中的 Office 开发&#41;](../vsto/publish-page-project-designer-office-development-in-visual-studio.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)