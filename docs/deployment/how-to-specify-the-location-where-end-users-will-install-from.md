---
title: 如何：指定最终用户将从中进行安装的位置 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], specifying an installation URL
- URLs, specifying an installation URL
- installation, specifying installation an URL
- Installation URL property
ms.assetid: 04a804bf-ed55-4a7a-a1e6-f63ed99c0276
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 993c654ccd16f2d51d86a46a716edd611ae154dd
ms.sourcegitcommit: bf2e9d4ff38bf5b62b8af3da1e6a183beb899809
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2020
ms.locfileid: "77557614"
---
# <a name="how-to-specify-the-location-where-end-users-will-install-from"></a>如何：指定最终用户将从中进行安装的位置
发布 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，用户下载和安装应用程序的位置并不一定是最初发布应用程序的位置。 例如，在某些组织中，开发人员可能会将应用程序发布到暂存服务器，然后管理员会将该应用程序移动到 Web 服务器。

在这种情况下，你可以使用 `Installation URL` 属性指定用户将在其中下载应用程序的 Web 服务器。 这是必需的，以便应用程序清单知道在何处查找更新。

`Installation URL` 属性可以在 "**项目设计器**" 的 "**发布**" 页上进行设置。

> [!NOTE]
> 还可以使用**发布向导**设置 `Installation URL` 属性。 有关详细信息，请参阅[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

### <a name="to-specify-an-installation-url"></a>指定安装 URL

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 在 "安装 URL" 字段中，使用格式 `https://www.contoso.com/ApplicationName`或 UNC 路径（格式为 `\Server\ApplicationName`）输入安装位置。

## <a name="see-also"></a>另请参阅
- [如何：指定 Visual Studio 复制文件的位置](../deployment/how-to-specify-where-visual-studio-copies-the-files.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)