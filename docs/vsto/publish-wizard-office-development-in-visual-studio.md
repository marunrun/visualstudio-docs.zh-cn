---
title: 发布向导 （在 Visual Studio 中的 Office 开发）
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
ms.openlocfilehash: 7879ad7cf18c3d09fddbab3923296e0896688af9
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63447070"
---
# <a name="publish-wizard-office-development-in-visual-studio"></a>发布向导 （在 Visual Studio 中的 Office 开发）
  使用**发布向导**若要将解决方案文件复制到指定位置，创建清单文件，并创建安装程序。

 若要访问此向导中，在**构建**菜单中，选择**发布** *SolutionName*。 您还可以访问**发布向导**从**解决方案资源管理器**。 打开项目节点的快捷菜单，然后选择**发布**。

 下面各部分介绍向导的页。

## <a name="where-do-you-want-to-publish-the-application"></a>要在其中发布应用程序？
 **指定要发布此应用程序的位置**所需。 发布位置是目录，其中**发布向导**复制从生成的解决方案文件，例如清单、 程序集、 临时证书和其他文件。 你必须对此目录具有写权限。

 为磁盘路径、 文件共享、 FTP 站点或网站 URL 键入位置或单击**浏览**按钮以浏览的位置。 路径可以是以下格式：

- 标准中的相对或绝对路径 Windows 格式，例如 *C:\Deploy\MyApplication* 或 *\MyApplication* 。

- 通用命名约定 (UNC) 路径，如 *\\\ServerName\MyApplication\\* 。

- URL 的 web 站点，如 http://www.microsoft.com/MyApplication 。

  默认情况下，发布位置是 *http://localhost/projectname/* 如果您安装了 IIS，或如果这样做的 publish\ 目录不具有安装 IIS。

> [!NOTE]
> 如果目标计算机正在运行 Windows Vista，有更多注意事项。 必须是 Windows Vista 计算机上的管理员才能使用本地发布选项。 此外，默认位置始终是 *发布\\* 目录下，无论是否安装了 IIS。

## <a name="what-is-the-default-installation-path-on-end-user-computers"></a>最终用户计算机上的默认安装路径是什么？
 安装路径是可选的。 如果您愿意，可以稍后再设置安装路径。 有关详细信息，请参阅[如何：更改 Office 解决方案的安装路径](https://msdn.microsoft.com/d0eaa07b-2d72-4902-899f-2f9fb165b8fd)。

 安装路径是最终用户将在其中安装自定义项的目录。 这也是解决方案将用于检查更新的路径。 **发布向导**不会不将解决方案部署到此位置中，除非该路径中输入相同**指定要发布此应用程序的位置**前一页上的框。

 **从网站上**指定最终用户将按照用于安装解决方案的 URL。

 **从 UNC 路径或文件共享**指定最终用户将按照用于安装解决方案的 UNC 路径。

 **从 CD-ROM 或 DVD-ROM**此选项不需要的安装路径。

 Visual Studio 不会不刻录 CD 或 DVD。 您必须手动将输出复制到 CD 或 DVD。

## <a name="see-also"></a>请参阅
- [使用 ClickOnce 部署 Office 解决方案](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [发布页，项目设计器&#40;Visual Studio 中的 Office 开发&#41;](../vsto/publish-page-project-designer-office-development-in-visual-studio.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
